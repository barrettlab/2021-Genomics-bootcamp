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

### some super helpful links and UNIX tutorials:
  [A video tutorial by CPING's own James Beck, with his truly awesome Kentucky dialect](https://www.invasiongenomics.com/computing.html)<br>
  [A primer on UNIX and Perl](http://korflab.ucdavis.edu/Unix_and_Perl/current.html)<br>
  [UNIX for beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/)<br>
  [A much fancier and more useful guide than the one I wrote. I have used this for inspiration here!](https://bioinformaticsworkbook.org/Appendix/Unix/unix-basics-1.html#gsc.tab=0)<br>
  [GitHub Markdown language -- how I wrote this tutorial](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)


### Some basic, essential unix commands
1. Where am I? **pwd** = Print Working directory: This command tells you where you are in the directory structure
   ```bash
   pwd                    # Tells you your current directory
   tree /home/cbarrett    # This gives a graphical display of your directory structure
   ```   
2. How do I get someplace else?            Change Directory: **cd**
   ```bash
   cd
   ```
   #### Try the following -- note the space between cd and what follows:
   ```bash
   cd ~     # (country roads) Take me home, to my home folder: ~/cbarrett = /home/cbarrett
   cd .     # Take me to where I am
   cd ..    # Take me up one level
   cd /     # take me to the root directory
   cd -     # I had to find the passage back to the place I was before
   cd /data/cbarrett/Corallorhiza_2021_08_05/reads/filtered reads    # This is an **'absolute' path**. The initial '/' is the **root**, followed by /data/etc...
   cd ~/documents   # take me home, then into 'documents'
   cd ../.. # take me up two levels
   cd ../reads   # take me up one, then into 'reads'
   ```
   ####

3. What is in this directory?  **ls** = List
   ```bash
   ls        # LIST the contents of a directory
   ls -l     # list the 'long version' including file sizes, permissions, etc.
   ls -a     # list all contents, including hidden files
   ### there are numerous 'flags' or 'options' with each UNIX command (e.g. -a, -l, -m, etc.). 
   ### how do I know what these all mean and which ones to use?  --> 'man'! 'man' takes you to the manual for each command.
   man ls
   man pwd   # etc...
   ```
  
4. How do I make a new directory?  **mkdir** = Make Directory
   ```bash
   mkdir genomics_class   # make a new directory
   mkdir genomics_class bioinformatics_class evolution_class    # make three new directories
   ```
5. How do I make a new, blank text file?  **touch**
   ```bash
   touch file1.txt file2.txt file3.txt   # make three new text files
   ```
6. How do I print something to the screen? **cat** = catalog or concatenate (depends on who you ask)
   #### to print the conents of a file to the screen:
   ```bash
   cat file1.txt                          # prints the contents of file1 to screen
   cat file1.txt file2.txt file3.txt      # prints files 1,2 and 3 to screen
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
11. How do I move a file or directory to another location? **mv**. How do I **locate** or **find** files, or files that contain specific text?
   ```bash
   mv file1.txt /data/cbarrett/evolution_class        # this command moves file1 into the evolution class folder. We specify the relative path for the files, because           
                                                      # we are already in the directory where it sits, and the full or absolute path to the destination directory
   ### OK, so I moved a file to another directory, but now I can't find it!
   locate file1.txt
   find /data/cbarrett -name *.txt                    # find all text files in /data/cbarrett using a wildcard
   find /data/cbarrett f -name ">*"                   # find all files in /data/cbarrett that contain a caret '>' e.g. all fasta files
   ```
12. We can also move a file from one directory to another without being in that particular directory
   ```bash
   mv /data/cbarrett/genomics_class/file1.txt /data/cbarrett/evolution_class
   ### mv can also be used to rename files
   mv file1.txt my_file1.txt     # This renames file1 my_file1
   ```
## Use extreme caution with 'mv'! Once you move it, it is gone, and you had better know where it is! Same goes for renaming files

13. Instead we can COPY files to another location: **cp**
```bash
cp file1.txt /data/cbarrett/evolution_class
```
14. And now for the DEADLIEST command in UNIX:  **rm**
## This command (rm) removes a file. Once it is gone, it is gone. there is no trash or recycle bin!
```bash
rm file1.txt              # removes a single file from existence
rm -R genomics_class      # removes a directory from existence
rm file1.txt file2.txt    # removes 2 files
rm -i file1.txt file2.txt # "playing it safe" with interactive mode. This will prompt you y/n before removing each file listed
rm -I *.txt               # Prompt once before removing more than three files
```
15. What if I want to copy all text files (.txt) or fasta (.fasta) into a new directory?  **'*'** = WILDCARD.
```bash
cp *.txt /data/cbarrett/evolution_class                                     # copy all text files to a new dir
cp /data/cbarrett/genomics_class/*.txt /data/cbarrett/evolution_class       # same command using absolute paths
cp * /data/cbarrett/evolution_class                                         # copy all files from current dir to a new dir
cp *1*.txt /data/cbarrett/evolution_class                                   # copy all files containing a '1' in the name to a new dir
```
16. Sorting files, counting, etc.
[Taken from here](https://bioinformaticsworkbook.org/Appendix/Unix/unix-basics-1.html#gsc.tab=0)
```bash
### Word count -- wc
wc file1.txt      # count the number of "words" i.e. characters in a file
wc -l file1.txt   # count the number of LINES in a file. Uses: how many reads are in a fasta file (divide by 2)
wc -c file1.txt   # count # of characters, but more specific notation
wc -w file1.txt   # count # words in a file
wc -l file1.txt > words_in_file1.txt    # count # lines in file1, redirect to new file with the output
wc -l file1.txt | less                  # count # lines in file 1, but 'pipe' the command to 'less. This is how we start building pipelines!
### Translate -- tr
tr '_' ' ' < file1.txt > file2.txt      # translate all underscores in file1 to spaces, and redirect to file 2. The less than sign directs INPUT. The greater than sign directs OUTPUT
shuf file1.txt > file2.txt              # randomize the lines in file1, output to file2
sort -g file1.txt | head                # sort the lines in file1, pipe to 'head' to view. the '-g' = 'general, which avoids 10 coming after 1 instead of 2.
uniq file1.txt | cat                    # pick out all the unique lines of file1
cat uniq file1.txt                      # does the same thing as above
sort -g file1.txt | uniq | wc -l | less     # sort lines in file1, find unique lines, count the # of unique lines, and display with 'less'
sort -g file1.txt | uniq -c | wc -l | less  # sort lines in file1, find unique lines and how many of each, count the # of unique lines, and display with 'less'
### OK, now let's get a little fancier...
cat file1.txt | tr ' ' '\n' | sort | uniq -c | sort -n | tail -n 4
### What did we do here?
cat file1.txt                                                               # show or print contents of file1 to screen
cat file1.txt | tr ' ' '\n'                                                 # now, translate all spaces to new lines (\n = newline)
cat file1.txt | tr ' ' '\n' | sort                                          # now, sort all the new lines
cat file1.txt | tr ' ' '\n' | sort | uniq -c                                # now, count all unique lines and how many of each
cat file1.txt | tr ' ' '\n' | sort | uniq -c | sort -n                      # now, sort each unique line based on the the frequency of each
cat file1.txt | tr ' ' '\n' | sort | uniq -c | sort -n | tail -n 4          # now, look at the last 4 lines to see the most common ones
```

17. Grep and Regular Expressions (RegEx). 
### Here is where we start to get into **REGULAR EXPRESSIONS**. A lot of bioinformatics = fancy regular expressions.
```bash
### general syntax for 'grep'

grep -flag PATTERN FILENAME
```
### GREP flags
[Borrowed from Here](https://bioinformaticsworkbook.org/Appendix/Unix/unix-basics-3grep.html#gsc.tab=0)
Argument | Function
-------- | --------
-v | inverts the match or finds lines NOT containing the pattern.
--color | colors the matched text for easy visualization
-F | interprets the pattern as a literal string.
-H,-h | print, don’t print the matched filename
-i | ignore case for the pattern matching.
-l | lists the file names containing the pattern (instead of match).
-n | prints the line number containing the pattern (instead of match).
-c | counts the number of matches for a pattern
-o | only print the matching pattern
-w | forces the pattern to match an entire word.
-x | forces patterns to match the whole line.

```bash
grep -c ">" rbcL4.fasta | less						# find all fasta header lines, count them (-c), and pipe to less
grep -e ">" rbcL4.fasta | less						# find all fasta header lines, (-e = exact match), and pipe to less
grep -e ">" rbcL4.fasta > rbcL_headers.txt			# find all fasta header lines, and redirect to new file
grep -v ">" rbcL4.fasta | less						# find all sequence line lines, (-v = anti-match), and pipe to less
grep --color "ATG" rbcL4.fasta 						# highlight all search matches

grep 'pattern1|pattern2|pattern3' FILENAME			# Any one pattern of the three (OR)
grep 'pattern1' FILENAME | grep 'pattern2' | grep 'pattern3'		# All three patterns (AND)

grep -rl "PATTERN" .								# find all files that contain a pattern (-r) in the current dir (.)
```

### REGULAR EXPRESSION GUIDE
[Borrowed from here](https://www.grymoire.com/Unix/Regular.html)<br>
### Anchors
Regular expression | Matches:
------------------ | --------
^A | "A" at the beginning of a line
A$ | "A" at the end of a line
A^ | "A^" anywhere on a line
$A | "$A" anywhere on a line
^^ | "^" at the beginning of a line
$$ | "$" at the end of a line


### Number matches
Regular Expression | Matches
------------------ | --------
[] | The characters "[]"
[0] |	The character "0"
[0-9] |	Any number
[^0-9] |	Any character other than a number
[-0-9] |	Any number or a "-"
[0-9-] |	Any number or a "-"
[^-0-9] | Any character except a number or a "-"
[]0-9] |	Any number or a "]"
[0-9]] |	Any number followed by a "]"
[0-9-z] | Any number, or any character between "9" and "z".
[0-9\-a\]] |	Any number, or a "-", a "a", or a "]". 
"\\" | This is called an **escape character**. 


### Wildcards, "anything" matches, and letter & number matches
Regular Expression | Matches
------------------ | -------
\* | Any line with an asterisk
\\* | Any line with an asterisk
\\\ | Any line with a backslash
^\* | Any line starting with an asterisk
^A\* | Any line
^A\\* | Any line starting with an "A*"
^AA* | Any line if it starts with one "A"
^AA\*B | Any line with one or more "A"'s followed by a "B"
^A\{4,8\\}B | Any line starting with 4, 5, 6, 7 or 8 "A"'s followed by a "B"
^A\\{4,\\}B | Any line starting with 4 or more "A"'s followed by a "B"
^A\\{4\\}B | Any line starting with "AAAAB"
\\{4,8\\} | Any line with "{4,8}"
A{4,8} | Any line with "A{4,8}"


### Other useful thing to know for regular expressions
Regular Expression | Class | Type | Meaning
------------------ | ----- | ---- | -------
. | all | Character Set | A single character (except newline)
^ | all | Anchor | Beginning of line
$ | all | Anchor | End of line
[...] | all | Character Set | Range of characters
\* | all | Modifier | zero or more duplicates
\\< | Basic | Anchor | Beginning of word
\\> | Basic | Anchor | End of word
\\(..\\) | Basic | Backreference | Remembers pattern
\\1..\\9 | Basic | Reference | Recalls pattern
\+ | Extended | Modifier | One or more duplicates
? | Extended | Modifier | Zero or one duplicate
\\{M,N\\} | Extended | Modifier | M to N Duplicates
(...\|...) | Extended | Anchor | Shows alteration
\\(...\\|...\\) | EMACS | Anchor | Shows alteration
\\w | EMACS | Character set | Matches a letter in a word
\\W | EMACS | Character set | Opposite of \\w

18. Searching, replacing, and "fishing" with: **grep**, **sed**, and **awk* 
#### These three commands will be among the most useful commands you ever learn. Actually, each is like a little language of its own
#### 18A. GREP = Global Regular Expression Print
[Here's a nice cheat sheet for GREPping](https://ryanstutorials.net/linuxtutorial/cheatsheetgrep.php)<br>

```bash
### General syntax for 'grep'
grep [options] [regexp] [filename]
```
#### 18B. SED = Stream Editor
```bash
### General syntax sor 'sed'
sed 'operation/regular_expression/replacement/flags' filename     # note the use of single quotes! The forward slash is the DELIMITER
sed 's/foo/bar/' file1.txt                                        # this directly changes all instances of 'foo' to 'bar' in file1. 
sed 's/foo/bar/' file1.txt > file2.txt                            # A safer alternative, that redirects the edited text to a new file2, while leaving file1 unchanged
### We can use regex just as with grep.
sed 's/\s/_/g' file1.txt > file2.txt                              # Replace all spaces (\s) with underscores. Note the use of '\' as an escape character, without it, it will remove 's' and replace with an underscore.
sed 's/\n/_/g' file1.txt > file2.txt                              # Replace all newlines (\n) with underscores. 
sed 's/\t/\s/g' file1.txt > file2.txt                             # Replace all newlines (\t) with spaces (\s).
sed 's/\([a-z]*\).*/\1/' file1.txt > file2.txt                    # You can also 'capture' what you find with (parentheses). Lets say you want to keep the first word you find in each line, then get rid of anything after that. (Think: I want to keep the first line of my fasta header but remove everything else)
### the '\1' = the first match pattern you found. The second is '\2' etc.

### The code below will do the following: 1) capture any pattern with 2 letters (and everything following), 2) then capture a second pattern with 2 letters and everything follwing, 3) substitute the second pattern for the first, and 4) substitute the first pattern for the second.
sed 's/\([a-z][a-z]*\) \([a-z][a-z]*\)/\2 \1/' file1.txt > file2.txt      


```
#### 18C. AWK = " Alfred Aho, Peter Weinberger, and Brian Kernighan" The authors who created it.

```bash

awk '{print $1}' file.fa > output.fa                          # capture the first "word" in fasta header, keep only that

### OK, so let's say we just downloaded an rbcL FASTA sequence from Genbank, and want to edit the FASTA header to look like this:
### Accesion.#_Genus_species

starting as:
>EU391360.1 Corallorhiza odontorhiza voucher Freudenstein 2778a atpB-rbcL intergenic spacer, partial sequence; ribulose-1,5-bisphosphate carboxylase/oxygenase large subunit (rbcL) gene, complete cds; and rbcL-accD intergenic spacer, partial sequence; chloroplast
TTGTTGTGAGAATTCTTAATTCATGAGTTGTAGGGAGGGACTTATGTCACCACAAACAGAAACTAAAGCA
AGCGTTGGATTTAAAGCTGGTGTTAAAGATTACAAATTGACTTATTATACTCCTGACTACGAAACCAAAG

### We can use awk to capture each space-separated 'field' in the header above:

awk '{print $1"_"$2"_"$3;next}1' rbcL.fasta > rbcL3.fasta    # here, we take a file downloaded from GenBank, and print the accession#, Genus, and species

Crap! it left a bunch of double underscores '__' a the end of each line of the sequence! Let's remove those with sed:

sed 's/__//g' rbcL3.fasta > rbcl4.fasta ; head rbcL4.fasta

We end up with:

>EU391360.1_Corallorhiza_odontorhiza
TTGTTGTGAGAATTCTTAATTCATGAGTTGTAGGGAGGGACTTATGTCACCACAAACAGAAACTAAAGCA
AGCGTTGGATTTAAAGCTGGTGTTAAAGATTACAAATTGACTTATTATACTCCTGACTACGAAACCAAAG

### If we want to keep the voucher information:
awk '{print $1"_"$2"_"$3"_"$5"_"$6;next}1' rbcL.fasta > rbcL3.fasta    # here, we take a file downloaded from GenBank, and print the accession#, Genus, and species
sed 's/__//g' rbcL3.fasta > rbcl4.fasta
head rbcL4.fasta

### We get:
>EU391360.1_Corallorhiza_odontorhiza_Freudenstein_2778a
TTGTTGTGAGAATTCTTAATTCATGAGTTGTAGGGAGGGACTTATGTCACCACAAACAGAAACTAAAGCA
AGCGTTGGATTTAAAGCTGGTGTTAAAGATTACAAATTGACTTATTATACTCCTGACTACGAAACCAAAG
```
