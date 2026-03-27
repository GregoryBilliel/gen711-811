## Gen711/811 Practical Exam 2023 (40 scaled points)

## NAME: Gregory Billiel

Instructions:  
- Make sure to paste all the commands that you use below each of the tasks.  
- Some tasks require you to copy your output here. All output that you paste is less than 10 lines.   
- Do not spend too much time on a single prompt. It's important to get to all prompts.    
- If you get stuck and do not know how to proceed: specifically ask for the answer.  
- Help will get you to the next step, but you will lose points for that prompt.  
- Questions on clarification of the question does not result in the loss of points.  
- Replace MYNAME with your first and last name.   
- Download the practical into your gen711/811 folder as indicated at the begining of class. 
- Keep the '.md' extension until you turn it in. 
- Right before you upload it, save it as a '.txt' document MYNAME_practical.txt. 
- Save the document to your lab folder so that you know where it is when you need to upload it.
- Document must be uploaded before 5pm to get credit. 

Hints: 
- Remember, if you want to re-run a command, but change it slightly to try to fix it, hit the up arrow and edit the last command that you ran. 
- When typing out commands, filenames, or paths, hit the tab button a couple time to see if it autocompletes for you

### 1. Paste the command(s) below that you used get practical exam pasted into vscode. (2 point)

Couldn't get it to work, nor did the rest of the class, just copy pasted the text file into the labs directory

### 2. From your home directory, make a new directory to hold fastq files called 'analysis' (2 points)

mkdir analysis (while in ~)

### 3. Copy the fastq files /tmp/gen711_2023/Sample1.fastq and /tmp/gen711_2023/Sample2.fastq directly into the 'analysis' directory without changing your current directory. (2 points, partial credit if you need to change directories first)
For todays practice practical, use SRR fastqs instead

cp ~/gen711-811/shell_data/untrimmed_fastq/SRR097977.fastq analysis

cp ~/gen711-811/shell_data/untrimmed_fastq/SRR098026.fastq analysis

cp ~/gen711-811/shell_data/untrimmed_fastq/*.fastq analysis (also pulled bad-reads.fastq, had to remove those from analysis, if we weren't pulling the fastq files we already have this may not be an issue)

### 4. Use an absolute path to change your current working directory to the 'analysis' folder/directory. (2 points, partial credit for using a relative path)

cd /home/users/gjb1039/analysis

### 5. The fastq file you just copied is data from the UNH genome center. This is the first time you've ever seen these FASTQs. To confirm that the format of the FASTQs look ok, view one of the two files and paste the top 4 lines of the file below. (4 points) 

head -4 SRR097977.fastq 

@SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
TATTCTGCCATAATGAAATTCGCCACTTGTTAGTGT
+SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
CCCCCCCCCCCCCCC>CCCCC7CCCCCCACA?5A5<

### 6. You've decided that you want to make a seperate file of the reads to BLAST them at NCBI to make sure they belong to the species that you seqiuenced. However, your blast program is written to accept FASTA files rather than FASTQ files (FASTA files only contain the header line above the read, and the read itself). You will need to make a 'FASTA' file from each FASTQ file. Before you make the new files, pipe the output to a command that that allows you to see just the first lines of the output. (5 points)  

grep -A1 --no-group-separator '^@SRR' SRR097977.fastq | head

displays the file, greps out the header lines based on the @SRR sequence and then includes the line right below it, head makes it so that it pulls up the first few lines. Remove the head part if you want to pipe the results into a new file

#### Hints: 
### FASTA only needs 2/4 lines that are in a FASTQ: 1) the header line that starts with '@' and 2) the sequence right after the header. However, the base call quality scores could contain '@' as well, which might lead to unwanted matches. 
### You can use the info in the header line to be very specific about what you are trying to match. 
### Add the '--no-group-separator' option to the other options of your command to keep the '--' out of the output

### 7. Redirect the output of your command (command in 6 that is converting the format of the FASTQ into FASTA) into new files. Give the new file the same names, but uses the '.fasta' extension rather than the '.fastq' extension of the original file name. (5 points)

grep -A1 --no-group-separator '^@SRR' SRR097977.fastq > SRR097977.fasta

put the result of the grep into a new file, got rid of the head pipe from question 6 because we want the whole file

Do another with the other file names

grep -A1 --no-group-separator '^@SRR' SRR098026.fastq > SRR098026.fasta

### 8. How many reads have 15 or more uncalled bases (NNNNNNNNNNNNNNN) in both samples? Count the number of reads in both WITHOUT making a new file. (4 points)

grep 'NNNNNNNNNNNNNNN' *.fasta | wc -l

got 100 reads, seems only SRR098026.fastq had any any bad reads

### 9. Make a new directory called 'to_blast' in your current directory. Then, move the two fasta files into this new 'to_blast' directory (4 points)

mkdir to_blast

mv *.fasta to_blast

### 10. Without changing directories, what command could you use to confirm that the files made it into the 'to_blast' folder. (2 points)

ls to_blast/ from our analysis directory

ls ~/analysis/to_blast/

### 11. What is the 100th line in the Sample1.fasta file? (hint: the 'head' command is one way to do this- but you may need to specify an option) (2 points)

head -100 SRR09977.fasta | tail -1

GCGGAGCTGGTGATTGGCGAACTGCTGCTGCTATTT

### 12. Run md5sum on Sample1.fasta (md5sum Sample1.fasta). Then, run it again, but redirect the output to a new file called 'my_md5sums.txt'.  (2 points)

md5sum SRR097977.fasta 

2fc2f7165ff31c0930a77909f20ba7c0  SRR097977.fasta

md5sum SRR097977.fasta > my_md5sums.txt

### 13. Next, run the md5sum command on Sample2.fasta and add it the the end of 'my_md5sums.txt'. (2 points)

md5sum SRR098026.fasta >> my_md5sums.txt 

### 14. Lastly, add your name to the end of 'my_md5sums.txt' file. (2 points)

echo Gregory Billiel >> my_md5sums.txt 

### Extra credit: Run fastqc on one of the fastq files, and one of the fasta files. Did they both run? Why or why not?  (2 points)

conda activate genomics

fastqc on fasta file, won't run because it lacks the quality score

