# Haplotig-purging
Here, I used the polished assembly.

<details>
  <summary><em>Asymmetron</em> purge_dups</summary>
  
  ### Mapping short reads using BWA MEM (BWA v0.7.17)
  1. Create an index
  ```
  bwa index asm.fasta
  ```
  Where `asm.fasta` is the polished assembly.
  
  2. Map short reads
  ```
  bwa mem -t 14 asm.fasta ASY_R1.fastq.gz ASY_R2.fastq.gz > out.sam
  ```
  Where `ASY_R1.fastq.gz` and `ASY_R2.fastq.gz` are forward (R1) and reverse (R2) reads.
  
  3. Convert output from `.sam` to `.bam`
  ```
  samtools view -S -b out.sam > out.bam
  ```
  ### purge_dups v1.2.5
  
  1. Calculate read depth histogram
  ```
  ./purge_dups/src/ngscstat out.bam
  ```
  Where `out.bam` is the output from the alignment step.
  
  2. Calculate base-level read depth
  ```
  ./purge_dups/bin/calcuts TX.stat > cutoffs 2>calcults.log
  ```
  The custom cutoffs are `5 38  62  75  125 225`
  
  3. Split an assembly and do a self-self alignment
  ```
  ./purge_dups/bin/split_fa asm.fasta > asm.split
  ```
  ```
  minimap2 -xasm20 -DP asm.split asm.split | gzip -c - > asm.split.self.paf.gz
  ```
  Where `asm.split` is the split assembly.
  
  4. Purge haplotigs and overlaps
  ```
  ./purge_dups/bin/purge_dups -2 -T cutoffs -c TX.base.cov asm.split.self.paf.gz > dups.bed 2> purge_dups.log
  ```
  Where `cutoffs` is a file containing the manually calculated cutoffs.
  
  5. Get purged primary and haplotig sequences.
  
  ```
  ./purge_dups/bin/get_seqs dups.bed asm.fasta
  ```
  Where `.bed` file `dups.bed` contains the coordinates for purging. Notice, `-e` was not included.
</details>


<details>
  <summary><em>Epigonichthys</em> purge_dups</summary>
  
  ### Mapping short reads using BWA MEM (BWA v0.7.17)
  1. Create an index
  ```
  bwa index asm.fasta
  ```
  Where `asm.fasta` is the polished assembly.
  
  2. Map short reads
  ```
  bwa mem -t 14 asm.fasta EPI_R1.fastq.gz EPI_R2.fastq.gz > out.sam
  ```
  Where `EPI_R1.fastq.gz` and `EPI_R2.fastq.gz` are forward (R1) and reverse (R2) reads.
  
  3. Convert output from `.sam` to `.bam`
  ```
  samtools view -S -b out.sam > out.bam
  ```
  ### purge_dups v1.2.5
  
  1. Calculate read depth histogram
  ```
  ./purge_dups/src/ngscstat out.bam
  ```
  Where `out.bam` is the output from the alignment step.
  
  2. Calculate base-level read depth
  ```
  ./purge_dups/bin/calcuts TX.stat > cutoffs 2>calcults.log
  ```
  The custom cutoffs are `5 84  84  85  85  225`
  
  3. Split an assembly and do a self-self alignment
  ```
  ./purge_dups/bin/split_fa asm.fasta > asm.split
  ```
  ```
  minimap2 -xasm20 -DP asm.split asm.split | gzip -c - > asm.split.self.paf.gz
  ```
  Where `asm.split` is the split assembly.
  
  4. Purge haplotigs and overlaps
  ```
  ./purge_dups/bin/purge_dups -2 -T cutoffs -c TX.base.cov asm.split.self.paf.gz > dups.bed 2> purge_dups.log
  ```
  Where `cutoffs` is a file containing the manually calculated cutoffs.
  
  5. Get purged primary and haplotig sequences.
  
  ```
  ./purge_dups/bin/get_seqs dups.bed asm.fasta
  ```
  Where `.bed` file `dups.bed` contains the coordinates for purging. Notice, `-e` was not included.
</details>

<details>
  <summary><em>B. lanceolatum</em> (North Sea) purge_dups</summary>
  
  ### Mapping short reads using Minimap2
  1. Map long reads
  ```
  minimap2 -x map-ont -t 12 asm.fasta /hps/nobackup/research/marioni/sodai/Blnc_canu_poly1/Blnc_canu_poly1.trimmedReads.fasta.gz | gzip -c - > asm.paf.gz
  ```
  Where `asm.fasta` is the polished assembly and `/hps/nobackup/research/marioni/sodai/Blnc_canu_poly1/Blnc_canu_poly1.trimmedReads.fasta.gz` is the full path to the Canu trimmed reads.
  
  ### purge_dups v1.2.5
  
  1. Calculate read depth histogram
  ```
  ./purge_dups/bin/pbcstat asm.paf.gz
  ```
  Where `asm.paf.gz` is the output from the alignment step.
  
  2. Calculate base-level read depth
  ```
  ./purge_dups/bin/calcuts -l 5 -m 28 -u 120 PB.stat > cutoffs 2>calcults.log
  ```
  Here, I set the custom cutoff.
  The custom cutoffs are `5 27  27  28  28  120`
  
  3. Split an assembly and do a self-self alignment
  ```
  ./purge_dups/bin/split_fa asm.fasta > asm.split
  ```
  ```
  minimap2 -xasm20 -DP asm.split asm.split | gzip -c - > asm.split.self.paf.gz
  ```
  Where `asm.split` is the split assembly.
  
  4. Purge haplotigs and overlaps
  ```
  ./purge_dups/bin/purge_dups -2 -T cutoffs -c PB.base.cov asm.split.self.paf.gz > dups.bed 2> purge_dups.log
  ```
  Where `cutoffs` is a file containing the manually calculated cutoffs.
  
  5. Get purged primary and haplotig sequences.
  
  ```
  ./purge_dups/bin/get_seqs dups.bed asm.fasta
  ```
  Where `.bed` file `dups.bed` contains the coordinates for purging. Notice, `-e` was not included.
</details>
