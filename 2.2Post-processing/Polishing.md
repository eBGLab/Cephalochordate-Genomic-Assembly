# Polishing of *Asymmetron*, *Epigonichthys* and *B. lanceolatum* (North Sea)

## Polishing with short reads
<details>
  <summary><em>Epigonichthys</em> POLCA</summary>
  
  ### POLCA (from MaSuRCA v3.4.2 toolkit)
  ```
  ./polca.sh \
  -a /hps/nobackup/research/marioni/sodai/EPI_masurca_LHE60_rerun/flye/assembly.fasta \
  -r '../../EPI_R1.fastq.gz ../../EPI_R2.fastq.gz' \
  -t 16 \
  -m 1G
  ```
  Where `EPI_R1.fastq.gz` and `EPI_R2.fastq.gz` are the forward (R1) and reverse (R2) short reads. `/hps/nobackup/research/marioni/sodai/EPI_masurca_LHE60_rerun/flye/assembly.fasta` is the full path to the assembly.
</details>

<details>
  <summary><em>Epigonichthys</em> POLCA</summary>
  
  ### POLCA (from MaSuRCA v3.4.2 toolkit)
  ```
  ./polca.sh \
  -a /hps/nobackup/research/marioni/sodai/ASY_masurca_Flye_m_para_LHE60_rerun/assembly.fasta \
  -r '../../ASY_R1.fastq.gz ../../ASY_R2.fastq.gz' \
  -t 16 \
  -m 1G
  ```
  Where `ASY_R1.fastq.gz` and `ASY_R2.fastq.gz` are the forward (R1) and reverse (R2) short reads. `/hps/nobackup/research/marioni/sodai/ASY_masurca_Flye_m_para_LHE60_rerun/assembly.fasta` is the full path to the assembly.
</details>

## Polishing with long reads

<details>
  <summary>Polishing with long reads</summary>
  
  ### Mapping long reads onto the assembly using Minimap2
  ```
  minimap2 \
  -x map-ont \
  -t 12 \
  asm.fasta \
  ../../Blnc_Feb20.fastq.gz | gzip -c - > asm.paf.gz
  ```
  Where `asm.fasta` is the assembly and `Blnc_Feb20.fastq.gz` is the long reads.
  ### Racon v1.4.3
  For this, I used the default parameters and the raw reads.
  ```
  racon \
  -t 15 \
  ../../Blnc_Feb20.fastq.gz \
  asm.paf.gz \
  asm.fasta > racon.fasta
  ```
  Where `asm.fasta` is the assembly, `Blnc_Feb20.fastq.gz` is the long reads and `asm.paf.gz` is the alignment file.
</details>

