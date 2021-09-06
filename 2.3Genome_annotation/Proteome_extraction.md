# Proteome extraction from BRAKER annotation.

<details>
  <summary>Annotated <em>Asymmetron</em></summary>
  
  ### Get CDS using `getAnnoFasta.pl` (BRAKER v2.1.6)
  ```
  getAnnoFasta.pl ../braker/braker.gtf --seqfile ../ASY_3_scaf.fa
  ```
  Where `ASY_3_scaf.fa` is the scaffolded genome and `braker.gtf` is the BRAKER annotation file.
  
  ### Use `transeq` from [EMBOSS](https://www.ebi.ac.uk/Tools/emboss/) to translate CDS
  ```
  transeq ../braker/braker.codingseq ASY.faa
  ```
  Where `braker.codingseq` is the output of the previous step.

</details>

<details>
  <summary>Annotated <em>Epigonichthys</em></summary>
    
  ### Get CDS using `getAnnoFasta.pl` (BRAKER v2.1.6)
  ```
  getAnnoFasta.pl ../braker/braker.gtf --seqfile ../EPI_2_scaf.fa
  ```
  Where `EPI_2_scaf.fa` is the scaffolded genome and `braker.gtf` is the BRAKER annotation file.
  
  ### Use `transeq` from [EMBOSS](https://www.ebi.ac.uk/Tools/emboss/) to translate CDS
  ```
  transeq ../braker/braker.codingseq EPI.faa
  ```
  Where `braker.codingseq` is the output of the previous step.
</details>

<details>
  <summary>Re-annotated <em>B. lanceolatum</em> from <a href="https://www.nature.com/articles/s41586-018-0734-6">Marlétaz et al. (2018)</a></summary>
  ### Get CDS using `getAnnoFasta.pl` (BRAKER v2.1.6)
  ```
  getAnnoFasta.pl ../braker/braker.gtf --seqfile ../../Blnc2018.fa
  ```
  Where `ASY_3_scaf.fa` is the scaffolded genome and `braker.gtf` is the BRAKER annotation file.
  
  ### Use `transeq` from [EMBOSS](https://www.ebi.ac.uk/Tools/emboss/) to translate CDS
  ```
  transeq ../braker/braker.codingseq Blnc2018_ET_all.faa
  ```
  Where `braker.codingseq` is the output of the previous step.
</details>
