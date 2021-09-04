# Long-read assembly of *B. lanceolatum* (North Sea)
Note: Due to poor performance of the genome annotation, this assembly was not used in downstream analysis.

<details>
  <summary><em>B. lanceolatum</em> (North Sea) Canu assembly with options to keep haplotypes</summary>
  
  ### Canu assembly (v2.1)
  Using the option to keep haplotypes, `corOutCoverage=200 "batOptions=-dg 3 -db 3 -dr 1 -ca 500 -cp 50"`.
  ```
  ./canu-2.1.1/bin/canu \
  -p Blnc_canu_poly1 \
  -d Blnc_canu_poly1 \
  genomeSize=500m \
  -nanopore Blnc_Feb20.fastq.gz \
  corOutCoverage=200 "batOptions=-dg 3 -db 3 -dr 1 -ca 500 -cp 50"
  ```
  Where `Blnc_Feb20.fastq.gz` is the base-called nanopore sequencing reads.
</details>
