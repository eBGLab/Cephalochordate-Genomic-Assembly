# Pre-assembly analysis

## Short reads

<details>
  <summary><em>Asymmetron</em></summary>
  
  * K-mer count histogram (Jellyfish v2.3.0)
  ```
  zcat ASY_R1.fastq.gz > ASY_R1.fastq
  zcat ASY_R2.fastq.gz > ASY_R2.fastq
  ```
  ```
  ./jellyfish count -C -m 21 -s 1000M -t 10 ASY_R1.fastq -o ASY_R1.jf
  ./jellyfish count -C -m 21 -s 1000M -t 10 ASY_R2.fastq -o ASY_R2.jf
  ```
  
  
  ```
  ./jellyfish histo -t 10 ASY_R1.jf > ASY_R1.histo
  ./jellyfish histo -t 10 ASY_R2.jf > ASY_R2.histo
  ```
  
  * K-mer spectra analysis (Genomescope v2.0)
  ```
  ```
  Where R1 and R2 are forward and reverse reads, respectively.
</details>

## Long reads

<details>
  <summary><em>Asymmetron</em></summary>
  
  * Visualising read lengths and quality (NanoPlot v1.38.1).
  ```
  NanoPlot \
  -t 8 \
  -o ONT_stats \
  -p ASY_log \
  --loglength \
  --N50 \
  --title "ASY" \
  --fastq ASY_all2_guppy4.fastq.gz
  ```
  Where `ASY_all2_guppy4.fastq.gz` is the name of the base-called nanopore sequencing reads.
</details>

<details>
  <summary><em>Epigonichthys</em></summary>
  
  * Visualising read lengths and quality (NanoPlot v1.38.1).
  ```
  NanoPlot \
  -t 8 \
  -o ONT_stats \
  -p EPI_log \
  --loglength \
  --N50 \
  --title "EPI" \
  --fastq EPI_all2_guppy4.fastq.gz
  ```
  Where `EPI_all2_guppy4.fastq.gz` is the name of the base-called nanopore sequencing reads.
</details>

<details>
  <summary><em>B. lanceolatum</em> (North Sea)</summary>
  
  * Visualising read lengths and quality (NanoPlot v1.38.1).
  ```
  NanoPlot \
  -t 8 \
  -o ONT_stats \
  -p Blnc_log \
  --loglength \
  --N50 \
  --title "Blnc" \
  --fastq Blnc_Feb20.fastq.gz
  ```
  Where `Blnc_Feb20.fastq.gz` is the name of the base-called nanopore sequencing reads.
</details>
