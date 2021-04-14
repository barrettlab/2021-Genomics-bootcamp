# 2021-Genomics-bootcamp

## Welcome to the 2021 WVU Genomic Bootcamp, part of the CPING Regional Network

### We will cover a number of topics here:
  Basic UNIX Commands<br>
  Manupilating text siles (fasta, fastq)<br>
  Basic shell scripting<br>
  Fastq files and data quality assessment<br>
  Quality and adapter trimming of Fastq files<br>
  Plastid genome assembly, finishing, and annotation<br>
  Plastome and multigene alignment<br>
  SNP processing, specifically using the ISSRseq plantform and data pipeline<br>
  Downstream phylogenetic and population genetic applications<br>

### Some basic, essential unix commands
1. Where am I?
   ```bash
   pwd
   ```
   #### Present Working directory: This command tells you where you are in the directory structure
   
2. How do I get someplace else?            Change Directory
   ```bash
   cd
   ```
   #### Try the following -- note the space between cd and what follows:
   ```bash
   cd ~     # Take me home (country roads)<br>
   cd.      # Take me to where I am<br>
   cd ..    # Take me up one level<br>
   cd /     # take me to the root directory<br>
   cd -     # take me to the place I was before<br>
   cd /data/cbarrett/Corallorhiza_2021_08_05/reads/filtered reads    # This is an 'absolute' path. The initial '/' is the root, followed by /data/etc...<br>
   cd ~/documents   # take me home, then into 'documents'<br>
   cd ../.. # take me up two levels<br>
   cd ../reads   # take me up one, then into 'reads'<br>
   ```
   ####

3. What is in this directory?  pwd
   ```bash
   ls        # LIST the contents of a directory<br>
   ls -l     # list the 'long version' including file sizes, permissions, etc.<br>
   ls -a     # list all contents, including hidden files<br>
   ```
  
4. How do I make a new directory?  mkdir
   ```bash
   mkdir genomics_class   # make a new directory
   mkdir genomics_class bioinformatics_class evolution_class    # make three new directories
   ```
5. How do I make a new, blank text file?  touch
   ```bash
   touch file1.txt file2.txt file3.txt   # make three new text files
   ```
6. How do I print something to the screen?
   #### to print the conents of a file to the screen:
   ```bash
   cat file1.txt
   ```
   #### OK, if there is a FASTQ file with > 1 million lines, cat isn't the way to go...
7. What if I want to scrool through a file?  less
   ```bash
   less file1.txt   # then, press space bar to scroll down one screen (page down)
   ```
8. What if I want to just look at the beginning or end of a file?  head   or   tail
   ```bash
   head file1.txt         # shows the 1st 100 lines of a file
   head -n 20 file1.txt   # shows the 1st 20 lines of a file
   tail -n 20 file1.txt   # shows the last 20 lines of a file
   ```
   
   
