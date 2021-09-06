# BRAKER annotation
Note: Due to poor performance of the *B. lanceolatum* (North Sea) genome annotation, this assembly was not used in downstream analysis.

## Annotation of the draft genomes of *Asymmetron* and *Epigonichthys*
<details>
  <summary><em>Asymmetron</em> Annotation using BRAKER ET mode</summary>
  
  ### Align RNA-seq reads using Hisat2
  
  1. Index the draft genome
  ```
  hisat2-build \
  ASY_3_scaf.fa \
  ASY_3_scaf
  ```
  Where `ASY_3_scaf.fa` is the scaffolded assembly (repeat-masked, haplotig-purged and polished).
  
  2. Map the RNA-seq reads
  ```
  hisat2 \
  -x ASY_3_scaf \
  -1 ../../RNA_preprocessing/ASY_RNA_R1_trimmed.fq.gz \
  -2 ../../RNA_preprocessing/ASY_RNA_R2_trimmed.fq.gz \
  -S input.sam
  ```
  Where `ASY_RNA_R1_trimmed.fq.gz` and `ASY_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads. For trimming protocol, see the [RNA-scaffolding step](https://github.com/eBGLab/Cephalochordate-Genomic-Assembly/blob/main/2.2Post-processing/RNA-scaffolding.md)
  
  3. Convert `.sam` to `.bam`
  ```
  samtools view -bS input.sam > input.bam
  ```
  4. Sort
  ```
  samtools sort -n -@ 4 -m 2G input.bam -o input.sorted.bam
  ```
  
  ### BRAKER ET mode (BRAKER v2.1.6)
  ```
  braker.pl \
  --species=ASY \
  --genome=ASY_3_scaf.fa \
  --bam=input.sorted.bam \
  --softmasking \
  --cores=20
  ```
  Where `input.sorted.bam` is the RNA-seq read alignment file and `ASY_3_scaf.fa` is the scaffolded assembly.
</details>

<details>
  <summary><em>Epigonichthys</em> Annotation using BRAKER ET mode</summary>
  
  ### Align RNA-seq reads using Hisat2
  
  1. Index the draft genome
  ```
  hisat2-build \
  EPI_2_scaf.fa \
  EPI_2_scaf
  ```
  Where `EPI_2_scaf.fa` is the scaffolded assembly (repeat-masked, haplotig-purged and polished).
  
  2. Map the RNA-seq reads
  ```
  hisat2 \
  -x EPI_2_scaf \
  -1 ../../RNA_preprocessing/EPI_RNA_R1_trimmed.fq.gz \
  -2 ../../RNA_preprocessing/EPI_RNA_R2_trimmed.fq.gz \
  -p 10 \
  -S input.sam
  ```
  Where `EPI_RNA_R1_trimmed.fq.gz` and `EPI_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads. For trimming protocol, see the [RNA-scaffolding step](https://github.com/eBGLab/Cephalochordate-Genomic-Assembly/blob/main/2.2Post-processing/RNA-scaffolding.md)
  
  3. Convert `.sam` to `.bam`
  ```
  samtools view -bS input.sam > input.bam
  ```
  4. Sort
  ```
  samtools sort -n -@ 4 -m 2G input.bam -o input.sorted.bam
  ```
  
  ### BRAKER ET mode (BRAKER v2.1.6)
  ```
  braker.pl \
  --species=EPI \
  --genome=EPI_2_scaf.fa \
  --bam=input.sorted.bam \
  --softmasking \
  --cores=20 \
  --useexisting
  --cores=20
  ```
  Where `input.sorted.bam` is the RNA-seq read alignment file and `EPI_2_scaf.fa` is the scaffolded assembly. I used `--useexisting` because the AUGUSTUS training parameter file `EPI` already exists from a previously failed run.
</details>

## Re-annotation of the published draft genome of *B. lanceolatum* from [Marlétaz et al. 2018](https://www.nature.com/articles/s41586-018-0734-6)

<details>
  <summary><em>B. lanceolatum</em> from Marlétaz et al. (2018)</summary>
  
  ### Align RNA-seq reads using Hisat2
  1. Remove white splaces in the fasta header
  ```
  sed 's, ,_,g'<Branchiostoma_lanceolatum.BraLan2.dna_sm.toplevel.fa >Blnc2018.fa
  ```
  Where `Branchiostoma_lanceolatum.BraLan2.dna_sm.toplevel.fa` is the downloaded draft genome.
  
  2. Index the draft genome
  ```
  hisat2-build \
  ../Blnc2018.fa \
  Blnc2018
  ```
  Where `Blnc2018.fa` is the published draft genome.
  
  3. Map the RNA-seq reads (adult + embryo)
  ```
  hisat2 \
  -x Blnc2018 \
  -1 ../../../Embryo_RNA_preprocessing/Blnc_all_RNA_R1_trimmed.fq \
  -2 ../../../Embryo_RNA_preprocessing/Blnc_all_RNA_R2_trimmed.fq \
  -p 10 \
  -S input.sam
  ```
  Where `Blnc_all_RNA_R1_trimmed.fq` and `Blnc_all_RNA_R2_trimmed.fq` are the forward (R1) and reverse (R2) trimmed RNA-seq reads from both adult and embryo. The embryo reads were trimmed using trimmomatic, i.e.
  ```
  trimmomatic PE \
  -threads 10 \
  -trimlog fastqc2.log \
  Blnc_EMBRYO_RNA_R1_raw.fastq \
  Blnc_EMBRYO_RNA_R2_raw.fastq \
  Blnc_EMBRYO_RNA_R1_trim_2.fq.gz \
  Blnc_EMBRYO_RNA_R1_unpaired_2.fq.gz \
  Blnc_EMBRYO_RNA_R2_trim_2.fq.gz \
  Blnc_EMBRYO_RNA_R2_unpaired_2.fq.gz \
  ILLUMINACLIP:adapter.fa:4:30:10 \
  SLIDINGWINDOW:4:15 \
  MINLEN:36 \
  LEADING:3 \
  TRAILING:3
  ```
  The output was unzipped, i.e.
  ```
  gunzip -c Blnc_EMBRYO_RNA_R1_trim_2.fq.gz >Blnc_EMBRYO_RNA_R1_trim_2.fq
  ```
  ```
  gunzip -c Blnc_EMBRYO_RNA_R2_trim_2.fq.gz >Blnc_EMBRYO_RNA_R2_trim_2.fq
  ```
  ...and concatenated with the adult reads.
  ```
  cat Blnc_EMBRYO_RNA_R1_trim_2.fq Blnc_ADULT_RNA_R1_trim.fq > Blnc_all_RNA_R1_trimmed.fq
  ```
  ```
  cat Blnc_EMBRYO_RNA_R2_trim_2.fq Blnc_ADULT_RNA_R2_trim.fq > Blnc_all_RNA_R2_trimmed.fq
  ```
  Where `Blnc_ADULT_RNA_R1_trim.fq` and `Blnc_ADULT_RNA_R2_trim.fq` are the adult reads.
  
  4. Convert `.sam` to `.bam`
  ```
  samtools view -bS input.sam > input.bam
  ```
  5. Sort
  ```
  samtools sort -n -@ 4 -m 2G input.bam -o input.sorted.bam
  ```
  
  ### BRAKER ET mode (BRAKER v2.1.6)

  
  ```
  braker.pl \
  --species=Blnc2018_ET_adult_embryo_3 \
  --genome=../Blnc2018.fa \
  --bam=input.sorted.bam \
  --softmasking \
  --cores=20
  ```
  Where `input.sorted.bam` is the RNA-seq read alignment file and `Blnc2018.fa` is the scaffolded assembly.
</details>
