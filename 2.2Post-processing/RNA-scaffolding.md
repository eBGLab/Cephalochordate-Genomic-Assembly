# RNA-scaffolding

<details>
  <summary><em>Asymmetron</em> RNA-scaffolding (hybrid approach)</summary>
  
  ### Map RNA-seq reads using hisat2
  
  1. Hard-mask the soft-masked assembly
  
  ```
  sed '/^[^>]/s/[a-z]/N/g'<ASY_3_RM.fa >ASY_3_RM_hard.fa
  ```
  Where `ASY_3_RM.fa` is the repeat-masked (and polished and haplotig-purged) genome.
  
  2. Index hard-masked genome
  
  ```
  hisat2-build \
  ASY_3_RM_hard.fa \
  ASY_3_RM_hard
  ```
  3. Align RNA-seq reads
  ```
  hisat2 \
  -x ASY_3_RM_hard \
  -1 ../../RNA_preprocessing/ASY_RNA_R1_trimmed.fq.gz \
  -2 ../../RNA_preprocessing/ASY_RNA_R2_trimmed.fq.gz \
  -k 3 \
  -p 10 \
  --pen-noncansplice 1000000 \
  -S input.sam
  ```
  Where `ASY_RNA_R1_trimmed.fq.gz` and `ASY_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads, and `ASY_3_RM_hard` is the hard-masked assembly.
  These were trimmed using trimmomatic, i.e.
  ```
  trimmomatic PE \
  -threads 10 \
  -trimlog trim_ASY.log \
  ../ASY_RNA_R1_QC.fastq \
  ../ASY_RNA_R2_QC.fastq \
  ASY_RNA_R1_trimmed.fq.gz \
  ASY_RNA_R1_unpaired.fq.gz \
  ASY_RNA_R2_trimmed.fq.gz \
  ASY_RNA_R2_unpaired.fq.gz \
  ILLUMINACLIP:TruSeq2-PE.fa:4:30:10 \
  SLIDINGWINDOW:5:15
  ```
  Where `ASY_RNA_R1_QC.fastq` and `ASY_RNA_R2_QC.fastq` are the raw reads.
  
  ### P_RNA_scaffolder
  1. Run P_RNA_scaffolder on the soft-masked genome
  ```
  ./P_RNA_scaffolder/P_RNA_scaffolder_edit.sh \
  -d ../../P_RNA_scaffolder \
  -i input.sam \
  -j ASY_3_RM.fa \
  -F ../../RNA_preprocessing/ASY_RNA_R1_trimmed.fq.gz \
  -R ../../RNA_preprocessing/ASY_RNA_R2_trimmed.fq.gz \
  -t 10 \
  -o scaffold
  ```
  Where `input.sam` is the mapping file from the hard-masked genome, `ASY_3_RM.fa` is the soft-masked assembly, and `ASY_RNA_R1_trimmed.fq.gz` and `ASY_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads.
  The `P_RNA_scaffolder_edit.sh` has been edited.
  

</details>
  
  
  
  
<details>
  <summary><em>Epigonichthys</em> RNA-scaffolding (hybrid approach)</summary>
  
  ### Map RNA-seq reads using hisat2
  
  1. Hard-mask the soft-masked assembly
  
  ```
  sed '/^[^>]/s/[a-z]/N/g'<EPI_2_RM.fa >EPI_2_RM_hard.fa
  ```
  Where `EPI_2_RM.fa` is the repeat-masked (and polished and haplotig-purged) genome.
  
  2. Index hard-masked genome
  
  ```
  hisat2-build \
  EPI_2_RM_hard.fa \
  EPI_2_RM_hard
  ```
  3. Align RNA-seq reads
  ```
  hisat2 \
  -x EPI_2_RM_hard \
  -1 ../../RNA_preprocessing/EPI_RNA_R1_trimmed.fq.gz \
  -2 ../../RNA_preprocessing/EPI_RNA_R2_trimmed.fq.gz \
  -k 3 \
  -p 10 \
  --pen-noncansplice 1000000 \
  -S input.sam
  ```
  Where `EPI_RNA_R1_trimmed.fq.gz` and `EPI_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads, and `EPI_2_RM_hard` is the hard-masked assembly.
  These were trimmed using trimmomatic, i.e.
  ```
  trimmomatic PE \
  -threads 10 \
  -trimlog trim_EPI.log \
  ../EPI_RNA_R1_QC.fastq \
  ../EPI_RNA_R2_QC.fastq \
  EPI_RNA_R1_trimmed.fq.gz \
  EPI_RNA_R1_unpaired.fq.gz \
  EPI_RNA_R2_trimmed.fq.gz \
  EPI_RNA_R2_unpaired.fq.gz \
  ILLUMINACLIP:TruSeq2-PE.fa:4:30:10 \
  SLIDINGWINDOW:5:15
  ```
  Where `EPI_RNA_R1_QC.fastq` and `EPI_RNA_R2_QC.fastq` are the raw reads.
  
  ### P_RNA_scaffolder
  1. Run P_RNA_scaffolder on the soft-masked genome
  ```
  ./P_RNA_scaffolder/P_RNA_scaffolder_edit.sh \
  -d ../../P_RNA_scaffolder \
  -i input.sam \
  -j EPI_2_RM.fa \
  -F ../../RNA_preprocessing/EPI_RNA_R1_trimmed.fq.gz \
  -R ../../RNA_preprocessing/EPI_RNA_R2_trimmed.fq.gz \
  -t 10 \
  -o scaffold
  ```
  Where `input.sam` is the mapping file from the hard-masked genome, `EPI_2_RM.fa` is the soft-masked assembly, and `EPI_RNA_R1_trimmed.fq.gz` and `EPI_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads.
  The `P_RNA_scaffolder_edit.sh` has been edited.

</details>  
