# Hybrid assembly of *Asymmetron* and *Epigonichthys*

<details>
  <summary><em>Asymmetron</em> MaSuRCA + Flye v2.8.2</summary>
  
  ### MaSuRCA config file
  ```
  DATA
  #Illumina paired end reads supplied as <two-character prefix> <fragment mean> <fragment stdev> <forward_reads> <reverse_reads>
  #if single-end, do not specify <reverse_reads>
  #MUST HAVE Illumina paired end reads to use MaSuRCA
  PE= pe 330 100  /hps/nobackup/research/marioni/sodai/ASY_R1.fastq.gz  /hps/nobackup/research/marioni/sodai/ASY_R2.fastq.gz
  #Illumina mate pair reads supplied as <two-character prefix> <fragment mean> <fragment stdev> <forward_reads> <reverse_reads>
  #JUMP= sh 3600 200  /FULL_PATH/short_1.fastq  /FULL_PATH/short_2.fastq
  #pacbio OR nanopore reads must be in a single fasta or fastq file with absolute path, can be gzipped
  #if you have both types of reads supply them both as NANOPORE type
  #PACBIO=/FULL_PATH/pacbio.fa
  NANOPORE=/hps/nobackup/research/marioni/sodai/ASY_all2_guppy4.fastq.gz
  #Other reads (Sanger, 454, etc) one frg file, concatenate your frg files into one if you have many
  #OTHER=/FULL_PATH/file.frg
  #synteny-assisted assembly, concatenate all reference genomes into one reference.fa; works for Illumina-only data
  #REFERENCE=/FULL_PATH/nanopore.fa
  END

  PARAMETERS
  #PLEASE READ all comments to essential parameters below, and set the parameters according to your project
  #set this to 1 if your Illumina jumping library reads are shorter than 100bp
  EXTEND_JUMP_READS=0
  #this is k-mer size for deBruijn graph values between 25 and 127 are supported, auto will compute the optimal size based on the read data and GC content
  GRAPH_KMER_SIZE = auto
  #set this to 1 for all Illumina-only assemblies
  #set this to 0 if you have more than 15x coverage by long reads (Pacbio or Nanopore) or any other long reads/mate pairs (Illumina MP, Sanger, 454, etc)
  USE_LINKING_MATES = 0
  #specifies whether to run the assembly on the grid
  USE_GRID=0
  #specifies grid engine to use SGE or SLURM
  #GRID_ENGINE=SGE
  #specifies queue (for SGE) or partition (for SLURM) to use when running on the grid MANDATORY
  #GRID_QUEUE=all.q
  #batch size in the amount of long read sequence for each batch on the grid
  #GRID_BATCH_SIZE=500000000
  #use at most this much coverage by the longest Pacbio or Nanopore reads, discard the rest of the reads
  #can increase this to 30 or 35 if your reads are short (N50<7000bp)
  LHE_COVERAGE=60
  #set to 0 (default) to do two passes of mega-reads for slower, but higher quality assembly, otherwise set to 1
  MEGA_READS_ONE_PASS=0
  #this parameter is useful if you have too many Illumina jumping library mates. Typically set it to 60 for bacteria and 300 for the other organisms
  #LIMIT_JUMP_COVERAGE = 300
  #these are the additional parameters to Celera Assembler.  do not worry about performance, number or processors or batch sizes -- these are computed automatically.
  #CABOG ASSEMBLY ONLY: set cgwErrorRate=0.25 for bacteria and 0.1<=cgwErrorRate<=0.15 for other organisms.
  #CA_PARAMETERS =  cgwErrorRate=0.15
  #CABOG ASSEMBLY ONLY: whether to attempt to close gaps in scaffolds with Illumina  or long read data
  #CLOSE_GAPS=1
  #number of cpus to use, set this to the number of CPUs/threads per node you will be using
  NUM_THREADS = 32
  #this is mandatory jellyfish hash size -- a safe value is estimated_genome_size*20
  JF_SIZE = 5000000000
  #ILLUMINA ONLY. Set this to 1 to use SOAPdenovo contigging/scaffolding module.
  #Assembly will be worse but will run faster. Useful for very large (>=8Gbp) genomes from Illumina-only data
  SOAP_ASSEMBLY=0
  #If you are doing Hybrid Illumina paired end + Nanopore/PacBio assembly ONLY (no Illumina mate pairs or OTHER frg files).
  #Set this to 1 to use Flye assembler for final assembly of corrected mega-reads.
  #A lot faster than CABOG, AND QUALITY IS THE SAME OR BETTER.
  #Works well even when MEGA_READS_ONE_PASS is set to 1.
  #DO NOT use if you have less than 15x coverage by long reads.
  FLYE_ASSEMBLY=1
  END
  ```
  
  ### MaSuRCA assembly (v3.4.2)
  
  ### Flye assembly
</details>

<details>
  <summary><em>Epigonichthys</em> MaSuRCA</summary>

  ### MaSuRCA config file
  ```
  DATA
  #Illumina paired end reads supplied as <two-character prefix> <fragment mean> <fragment stdev> <forward_reads> <reverse_reads>
  #if single-end, do not specify <reverse_reads>
  #MUST HAVE Illumina paired end reads to use MaSuRCA
  PE= pe 330 100  /hps/nobackup/research/marioni/sodai/EPI_R1.fastq.gz  /hps/nobackup/research/marioni/sodai/EPI_R2.fastq.gz
  #Illumina mate pair reads supplied as <two-character prefix> <fragment mean> <fragment stdev> <forward_reads> <reverse_reads>
  #JUMP= sh 3600 200  /FULL_PATH/short_1.fastq  /FULL_PATH/short_2.fastq
  #pacbio OR nanopore reads must be in a single fasta or fastq file with absolute path, can be gzipped
  #if you have both types of reads supply them both as NANOPORE type
  #PACBIO=/FULL_PATH/pacbio.fa
  NANOPORE=/hps/nobackup/research/marioni/sodai/EPI_all2_guppy4.fastq.gz
  #Other reads (Sanger, 454, etc) one frg file, concatenate your frg files into one if you have many
  #OTHER=/FULL_PATH/file.frg
  #synteny-assisted assembly, concatenate all reference genomes into one reference.fa; works for Illumina-only data
  #REFERENCE=/FULL_PATH/nanopore.fa
  END

  PARAMETERS
  #PLEASE READ all comments to essential parameters below, and set the parameters according to your project
  #set this to 1 if your Illumina jumping library reads are shorter than 100bp
  EXTEND_JUMP_READS=0
  #this is k-mer size for deBruijn graph values between 25 and 127 are supported, auto will compute the optimal size based on the read data and GC content
  GRAPH_KMER_SIZE = auto
  #set this to 1 for all Illumina-only assemblies
  #set this to 0 if you have more than 15x coverage by long reads (Pacbio or Nanopore) or any other long reads/mate pairs (Illumina MP, Sanger, 454, etc)
  USE_LINKING_MATES = 0
  #specifies whether to run the assembly on the grid
  USE_GRID=0
  #specifies grid engine to use SGE or SLURM
  #GRID_ENGINE=SGE
  #specifies queue (for SGE) or partition (for SLURM) to use when running on the grid MANDATORY
  #GRID_QUEUE=all.q
  #batch size in the amount of long read sequence for each batch on the grid
  #GRID_BATCH_SIZE=500000000
  #use at most this much coverage by the longest Pacbio or Nanopore reads, discard the rest of the reads
  #can increase this to 30 or 35 if your reads are short (N50<7000bp)
  LHE_COVERAGE=60
  #set to 0 (default) to do two passes of mega-reads for slower, but higher quality assembly, otherwise set to 1
  MEGA_READS_ONE_PASS=0
  #this parameter is useful if you have too many Illumina jumping library mates. Typically set it to 60 for bacteria and 300 for the other organisms
  #LIMIT_JUMP_COVERAGE = 300
  #these are the additional parameters to Celera Assembler.  do not worry about performance, number or processors or batch sizes -- these are computed automatically.
  #CABOG ASSEMBLY ONLY: set cgwErrorRate=0.25 for bacteria and 0.1<=cgwErrorRate<=0.15 for other organisms.
  #CA_PARAMETERS =  cgwErrorRate=0.15
  #CABOG ASSEMBLY ONLY: whether to attempt to close gaps in scaffolds with Illumina  or long read data
  #CLOSE_GAPS=1
  #number of cpus to use, set this to the number of CPUs/threads per node you will be using
  NUM_THREADS = 32
  #this is mandatory jellyfish hash size -- a safe value is estimated_genome_size*20
  JF_SIZE = 10000000000 #500mb*20
  #ILLUMINA ONLY. Set this to 1 to use SOAPdenovo contigging/scaffolding module.
  #Assembly will be worse but will run faster. Useful for very large (>=8Gbp) genomes from Illumina-only data
  SOAP_ASSEMBLY=0
  #If you are doing Hybrid Illumina paired end + Nanopore/PacBio assembly ONLY (no Illumina mate pairs or OTHER frg files).
  #Set this to 1 to use Flye assembler for final assembly of corrected mega-reads.
  #A lot faster than CABOG, AND QUALITY IS THE SAME OR BETTER.
  #Works well even when MEGA_READS_ONE_PASS is set to 1.
  #DO NOT use if you have less than 15x coverage by long reads.
  FLYE_ASSEMBLY=1
  END
  ```
  
  ### MaSuRCA assembly (v3.4.2)
  ```
  ./masurca sr_config_epi_lhe60.txt
  ```
  Where `sr_config_epi_lhe60.txt` is the config file for *Epigonichthys* with option `LHE_COVERAGE=60`. This generates a configuration shell script `assembly.sh`, which is run to assemble the data.
  ```
  ./assemble.sh
  ```
</details>
