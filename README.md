# 2021-Genomics-bootcamp

## Welcome to the 2021 WVU Genomic Bootcamp, part of the CPING Regional Network

### We will cover a number of topics here:
  Basic UNIX Commands
  Manupilating text siles (fasta, fastq)
  Basic shell scripting
  Fastq files and data quality assessment
  Quality and adapter trimming of Fastq files
  Plastid genome assembly, finishing, and annotation
  Plastome and multigene alignment
  SNP processing, specifically using the ISSRseq plantform and data pipeline
  Downstream phylogenetic and population genetic applications

### Some basic, essential unix commands
#### 1. Where am I?
   pwd
   #### Present Working directory: This command tells you where you are in the directory structure
   
#### 2. How do I get someplace else?
   cd
   
   #### Try the following -- note the space between cd and what follows:
   cd ~     # Take me home (country roads)
   cd.      # Take me to where I am
   cd ..    # Take me up one level
   cd /     # take me to the root directory
   cd -     # take me to the place I was before
   cd /data/cbarrett/Corallorhiza_2021_08_05/reads/filtered reads    # This is an 'absolute' path. The initial '/' is the root, followed by /data/etc...
   cd ~/documents   # take me home, then into 'documents'
   cd ../.. # take me up two levels
   cd ../reads   # take me up one, then into 'reads'
   #### Change Directory
  
