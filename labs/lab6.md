---
title: "Lab 6"
author: "Jeffrey Miller"
date: "2026 Feb 27"
output: pdf_document
---

### MY NOTES

ls -lrth: lists files with human readable sizes smallest to largest

which: tells you where a command is in ron, is you do "which cp" it will tell you where the copy command is (/usr/bin/cp)

conda activate genomics: activates the genomics conda environment

ctrl + r: lets you reverse search previous commands

history | grep conda: goes through your history and looks for commands where you used conda and lists them

>: similar to pipe but is redirect, it is like piping to a location. Can do something like "history > [file name]" to put the history into a new file or an existing one

/: starts an absolute pathway

>>: appends to the end of a file, so if we did "history >> [file name]" it would append our command history to the end of the file

ctrl + c: exits out if you accidentally mess up and get stuck in something like a "wc -l" command

grep -B[#] -A[#] [command]: shows the lines before and after the grepped line



### Today
1. Review, fastqc
2. Redirection and pipes lesson
3. Script writing

## review
which for programs
conda environments
chmod for permissions
fastqc


## keypoints
Employ the grep command to search for information within files.
Print the results of a command to a file.
Construct command pipelines with two or more stages.
Use for loops to run the same command for several input files.


## questions for practical
How can I search within files?
How can I combine existing commands to do new things?



## HELP: Nucleotide abbreviations
The four nucleotides that appear in DNA are abbreviated A, C, T and G. Unknown nucleotides are represented with the letter N. An N appearing in a sequencing file represents a position where the sequencing machine was not able to confidently determine the nucleotide in that position. You can think of an N as being aNy nucleotide at that position in the DNA sequence.


## Exercise 1

1. Search for the sequence `GNATNACCACTTCC` in the `SRR098026.fastq` file.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

grep -B1 GNATNACCACTTCC SRR098026.fastq

@SRR098026.245 HWUSI-EAS1599_1:2:1:2:801 length=35
GNATNACCACTTCCAGTGCTGANNNNNNNGGGATG

2. Search for the sequence `AAGTT` in both FASTQ files.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

grep -B1 AAGTT *.fastq

SRR097977.fastq-@SRR097977.11 209DTAAXX_Lenski2_1_7:8:3:247:351 length=36
SRR097977.fastq:GATTGCTTTAATGAAAAAGTCATATAAGTTGCCATG
--
SRR097977.fastq-@SRR097977.67 209DTAAXX_Lenski2_1_7:8:3:544:566 length=36
SRR097977.fastq:TTGTCCACGCTTTTCTATGTAAAGTTTATTTGCTTT
--
SRR097977.fastq-@SRR097977.68 209DTAAXX_Lenski2_1_7:8:3:724:110 length=36
SRR097977.fastq:TGAAGCCTGCTTTTTTATACTAAGTTTGCATTATAA
--
SRR097977.fastq-@SRR097977.80 209DTAAXX_Lenski2_1_7:8:3:258:281 length=36
SRR097977.fastq:GTGGCGCTGCTGCATAAGTTGGGTTATCAGGTCGTT
--
SRR097977.fastq-@SRR097977.92 209DTAAXX_Lenski2_1_7:8:3:353:318 length=36
SRR097977.fastq:GGCAAAATGGTCCTCCAGCCAGGCCAGAAGCAAGTT
--
SRR097977.fastq-@SRR097977.139 209DTAAXX_Lenski2_1_7:8:3:703:655 length=36
SRR097977.fastq:TTTATTTGTAAAGTTTTGTTGAAATAAGGGTTGTAA
--
SRR097977.fastq-@SRR097977.238 209DTAAXX_Lenski2_1_7:8:3:592:919 length=36
SRR097977.fastq:TTCTTACCATCCTGAAGTTTTTTCATCTTCCCTGAT
--
SRR098026.fastq-@SRR098026.158 HWUSI-EAS1599_1:2:1:1:1505 length=35
SRR098026.fastq:GNNNNNNNNCAAAGTTGATCNNNNNNNNNTGTGCG

3. How do the search results differ when matching in one file vs. both files? If you wanted to keep the original FASTQ format, how would you get around this?

When you search both files it lists the file name each line came from before their showed line

can use the "-v" option on grep that gets rid of the bad reads from the file and gives everything that doesn't pass the inverse grep

4. Make a file called 'bad-reads.fastq' made up of reads with 10 Ns or more in a row

grep -h -B1 -A2 NNNNNNNNNN *.fastq | grep -v '^--' > bad-reads.fastq

could also do: 

grep -h --no-group-separator -B1 -A2 NNNNNNNNNN *.fastq > bad-reads.fastq   (okay maybe not, this isn't working, just use the other one)

## Exercise 2

How many sequences are there in `SRR098026.fastq`? Remember that every sequence is formed by four lines.

just do word count on the file and divide by four

could also: 

grep '^@' [file name] | wc -l

This gets all the quality score lines and counts them

## Exercise 3

How many sequences in `SRR098026.fastq` contain at least 3 consecutive Ns?

Do grep for the NNN's, then pipe that into a wc command 

## Exercise 4

Print the file prefix of all of the `.txt` files in our current directory.

for fq in *.txt
> do
> basename "$fq"
> done

only listed the headline.txt file

## Exercise 5

After renaming the fastqs as demonstrated, remove `_2026` from all of the `.txt` files.

for filename in *.fastq
do 
echo -e "name=$

## Exercise 6

We want the script to tell us when it's done.

1. Open `bad-reads-script.sh` and add the line `echo "Script finished!"` after the `grep` command and save the file.
2. Run the updated script.




## keypoints

- `grep` is a powerful search tool with many options for customization.
- `>`, `>>`, and `|` are different ways of redirecting output.
- `command > file` redirects a command's output to a file.
- `command >> file` redirects a command's output to a file without overwriting the existing contents of the file.
- `command_1 | command_2` redirects the output of the first command as input to the second command.
- `for` loops are used for iteration.
- `basename` gets rid of repetitive parts of names.





```bash
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_2.fastq.gz
```
```bash
$ cd
$ wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```

or

```bash
$ cd
$ curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```

for name in *.fastq
do
echo ${name}
done

Basic version, for each time there is a file with .fastq, it will echo (print) the names

for name in *.fastq
do
name=$(basename ${filename} .fastq)
echo ${name}
done

This 

for fq in *.fastq
do 
wc -l ${fq}
done

FOO='this-is-a-var'

echo: just prints what you typed, put a dollar sign $ before the name to print what is inside it

for name in *.fastq
do
head -n 2 ${filename}
done

for filename in *.fastq
do
name=$(basename ${filename} .fastq)
mv ${filename} ${name}_2026.txt
done

renames and moves the fastq files, can put echo -e before the name and mv lines (put the lines in ") to test more safely