# *De novo* transcriptome assembly

<details>
  <summary><em>B. lanceolatum</em> (from Banyuls-sur-Mer) genome-guided</summary>
  
  I used the adult RNA-seq reads.
  ### Trinity v2.12.0 genome-guided mode
  ```
  Trinity \
  --genome_guided_bam /hps/nobackup/research/marioni/sodai/braker_results/Blnc/igv_sorted.bam \
  --genome_guided_max_intron 10000 \
  --seqType fq \
  --left ../RNA_preprocessing/Blnc_RNA_R1_trimmed.fq.gz \
  --right ../RNA_preprocessing/Blnc_RNA_R2_trimmed.fq.gz \
  --CPU 6 \
  --max_memory 20G \
  --output /hps/nobackup/research/marioni/sodai/trinity_results/trinity_guided_out_dir
  ```
  Where `Blnc_RNA_R1_trimmed.fq.gz` and `Blnc_RNA_R2_trimmed.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads. `igv_sorted.bam` is the sorted RNA-seq mapping (which was done for IGV), i.e.
  ```
  samtools sort input.bam -o igv_sorted.bam
  ```
</details>


<details>
  <summary><em>A. lucayanum</em> from <a href="https://academic.oup.com/gbe/article/6/10/2681/610856">Yue et al. (2014)</a></summary>
  
  ### Trinity v2.12.0
  ```
  Trinity \
  --seqType fq \
  --left /hps/nobackup/research/marioni/sodai/Yue2014/ASY_Yue_ADULT_RNA_R1_trim.fq.gz \
  --right /hps/nobackup/research/marioni/sodai/Yue2014/ASY_Yue_ADULT_RNA_R2_trim.fq.gz \
  --CPU 6 \
  --max_memory 20G \
  --output /hps/nobackup/research/marioni/sodai/trinity_results/trinity_Yue_adult_out_dir
  ```
  Where `ASY_Yue_ADULT_RNA_R1_trim.fq.gz` and `ASY_Yue_ADULT_RNA_R2_trim.fq.gz` are the forward (R1) and reverse (R2) trimmed RNA-seq reads from [Yue et al. (2014)](https://academic.oup.com/gbe/article/6/10/2681/610856). These were trimmed using trimmomatic, i.e.
  ```
  trimmomatic PE \
  -threads 30 \
  -trimlog trim_adult.log \
  asymmetron_Yue_ADULT_raw_1.fastq \
  asymmetron_Yue_ADULT_raw_2.fastq \
  ASY_Yue_ADULT_RNA_R1_trim.fq.gz \
  ASY_Yue_ADULT_RNA_R1_unpaired.fq.gz \
  ASY_Yue_ADULT_RNA_R2_trim.fq.gz \
  ASY_Yue_ADULT_RNA_R2_unpaired.fq.gz \
  ILLUMINACLIP:adapter.fa:4:30:10 \
  SLIDINGWINDOW:5:15
  ```
</details>
