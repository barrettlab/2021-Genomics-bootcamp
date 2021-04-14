# 2021-Genomics-bootcamp

## Welcome to the 2021 WVU Genomic Bootcamp, part of the CPING Regional Network!

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
1. Where am I? **pwd** = Present Working directory: This command tells you where you are in the directory structure
   ```bash
   pwd
   ```   
2. How do I get someplace else?            Change Directory: **cd**
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

3. What is in this directory?  **ls**
   ```bash
   ls        # LIST the contents of a directory<br>
   ls -l     # list the 'long version' including file sizes, permissions, etc.<br>
   ls -a     # list all contents, including hidden files<br>
   ```
  
4. How do I make a new directory?  **mkdir**
   ```bash
   mkdir genomics_class   # make a new directory
   mkdir genomics_class bioinformatics_class evolution_class    # make three new directories
   ```
5. How do I make a new, blank text file?  **touch**
   ```bash
   touch file1.txt file2.txt file3.txt   # make three new text files
   ```
6. How do I print something to the screen?
   #### to print the conents of a file to the screen:
   ```bash
   cat file1.txt
   ```
   #### OK, if there is a FASTQ file with > 1 million lines, cat isn't the way to go...
7. What if I want to scroll through a file?  **less**
   ```bash
   less file1.txt   # then, press space bar to scroll down one screen (page down) -- press *q* to exit 'less'
   ```
8. What if I want to just look at the beginning or end of a file?  **head**   or   **tail**
   ```bash
   head file1.txt         # shows the 1st 100 lines of a file
   head -n 20 file1.txt   # shows the 1st 20 lines of a file
   tail -n 20 file1.txt   # shows the last 20 lines of a file
   ```
9. How can I take the contents of a file and stick them into a new file? '**>**', or 'redirect, and '**>>**' or 'append'
   ```bash
   cat file1.txt > file2.txt                # stick the contents of file1 into a new file, called file2 (redirect)
   cat file2.txt file3.txt >> file1.txt     # stick the contents of files2 & 3 on the end of file1 (append)
   ```
10. How do I make a list of all files in a folder? This could be helpful to set up name files for running batch scripts on a directory full of 200 FASTQ files
   ```bash
   ls genomics_class > genomics_class_filenames.txt
   ```
11. How do I move a file or directory to another location? **mv**
   ```bash
   mv file1.txt /data/cbarrett/evolution_class        # this command moves file1 into the evolution class folder. We specify the relative path for the files, because           
                                                      # we are already in the directory where it sits, and the full or absolute path to the destination directory
   ```
12. We can also move a file from one directory to another without being in that particular directory
   ```bash
   mv /data/cbarrett/genomics_class/file1.txt /data/cbarrett/evolution_class
   ### mv can also be used to rename files
   mv file1.txt my_file1.txt     # This renames file1 my_file1
   ```
#### Use extreme caution with 'mv'! Once you move it, it is gone, and you had better know where it is! Same goes for renaming files

13. Instead we can COPY files to another location: **cp**
```bash
cp file1.txt /data/cbarrett/evolution_class
```
14. And now for the DEADLIEST command in UNIX:  **rm**
#### This command removes a file. Once it is gone, it is gone. there is no trash or recycle bin!
```bash
rm file1.txt              # removes a single file from existence
rm -R genomics_class      # removes a directory from existence
rm file1.txt file2.txt    # removes 2 files
```
15. What if I want to copy all text files (.txt) or fasta (.fasta) into a new directory?  **'*'** = WILDCARD.


