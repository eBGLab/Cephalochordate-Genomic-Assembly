# Repeat-masking

<details>
  <summary><em>Asymmetron</em> RM</summary>
  
  ### Repeat-masking using RepeatModeler and RepeatMasker (from TETools 1.3)
  1. Build database
  
  ```
  singularity exec docker://dfam/tetools:latest BuildDatabase \
  -name ASY \
  purged.fa
  ```
  Where `purged.fa` is the purged assembly.
  
  2. Model repeats using RepeatModeler
  
  ```
  singularity exec docker://dfam/tetools:latest RepeatModeler \
  -database ASY \
  -pa 6 \
  -LTRStruct
  ```
  3. Mask repeats using RepeatMasker
  ```
  singularity exec docker://dfam/tetools:latest RepeatMasker \
  -lib ASY-families.fa \
  purged.fa \
  -pa 6 \
  -xsmall
  ```
</details>

<details>
  <summary><em>Epigonichthys</em> RM</summary>
  
  ### Repeat-masking using RepeatModeler and RepeatMasker (from TETools 1.3)
  1. Build database
  
  ```
  singularity exec docker://dfam/tetools:latest BuildDatabase \
  -name EPI \
  purged.fa
  ```
  Where `purged.fa` is the purged assembly.
  
  2. Model repeats using RepeatModeler
  
  ```
  singularity exec docker://dfam/tetools:latest RepeatModeler \
  -database EPI \
  -pa 6 \
  -LTRStruct
  ```
  3. Mask repeats using RepeatMasker
  ```
  singularity exec docker://dfam/tetools:latest RepeatMasker \
  -lib EPI-families.fa \
  purged.fa \
  -pa 6 \
  -xsmall
  ```
</details>

<details>
  <summary><em>B. lanceolatum</em> (North Sea) RM</summary>
  
  ### Repeat-masking using RepeatModeler and RepeatMasker (from TETools 1.3)
  1. Build database
  
  ```
  singularity exec docker://dfam/tetools:latest BuildDatabase \
  -name Blnc \
  purged.fa
  ```
  Where `purged.fa` is the purged assembly.
  
  2. Model repeats using RepeatModeler
  
  ```
  singularity exec docker://dfam/tetools:latest RepeatModeler \
  -database Blnc \
  -pa 6 \
  -LTRStruct
  ```
  3. Mask repeats using RepeatMasker
  ```
  singularity exec docker://dfam/tetools:latest RepeatMasker \
  -lib Blnc-families.fa \
  purged.fa \
  -pa 6 \
  -xsmall
  ```
</details>
