---
title: "Lab 5"
author: "Jeffrey Miller"
date: "2026 Feb 20"
output: pdf_document
---

# MY NOTES

ls -lh: human readable, shows file size data

ls -l: long format to view file permissions

chmod: change mode, changes permissions

chmod -w [filename]: takes away write priv from the file, user only change

rm -rf: removes a directory/file and then everything in it cause it is recursive and forced



### Today
1. Review
2. Permissions
3. Conda environments
4. Running Fastqc
5. Redirection (if there is time)

:::::::::::::::::::::::::::::::::::::::: keypoints

- You can view file permissions using `ls -l` and change permissions using `chmod`.
- The `history` command and the up arrow on your keyboard can be used to repeat recently used commands.
- Conda environments simplify reporducability, dependencies and sharing environments.

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::: review

- You can view file contents using `less`, `cat`, `head` or `tail`.
- The commands `cp`, `mv`, and `mkdir` are useful for manipulating existing files and creating new directories.

### Quality scores. Highest score for a base is 41
Quality encoding: !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJ
                   |         |         |         |         |
Quality score:    01........11........21........31........41

::::::::::::::::::::::::::::::::::::::::::::::::::

*Warm ups: What is the last read in the SRR097977.fastq file? How confident are you in this read?
A: 

For SRR097977.fastq, the final read is for C with a quality score of 3 ($), so not very confident in the read which is normal as the end of sequencing is typically more prone to errors

How big are your fastqs? (Hint: Look at the options for the ls command to see how to show file sizes.)
- hint, it involves 'ls'. See if you can do it using a relative and absolute path
- another hint: There is an option to make it easy to read the file size. Use one of the two methods to find it
A:

ls -lh: human readable format to show file sizes

Whule in untrimmed_fastq, I just did ls -lh to see the file size for all of the files

Could do ls -lh SRR097977.fastq to specfically see the file in question (relative path)

ls -lh /home/users/gjb1039/gen711-811/shell_data/untrimmed_fastq/SRR097977.fastq  to view the size from wherever you are in your system (absolute path)

-rw-r--r--. 1 gjb1039 domain users 47K Jan 28 12:38 SRR097977.fastq

### EXERCISE 5.1
Starting in the shell_data/untrimmed_fastq directory, do the following:

Make sure that you have deleted your backup directory and all files it contains.
Create a backup of each of your FASTQ files using cp. (Note: You’ll need to do this individually for each of the two FASTQ files. We haven’t learned yet how to do this with a wildcard.)
Use a wildcard to move all of your backup files to a new backup directory.
Paste the code you used to do each step between the \'\'\' below:


```

I did mv *.fastq ../ to move the files from backup back out to untrimmed.fastq

I then did mv *_backup.fastq backup to move the backup files into the backup directory

(we already went through making backup together but its just mkdir backup then cp [filename] [backupfilename]/backup to make the files in backup or just cp [filename] [backupfilename] then mv *_backup.fastq to move the copy files into the backup directory)

can rename files with the mv command: mv [backupfilename] [sameplacebutwithnewfilename] (try and do it in the directory they are in so you can dodge having to put the pathway in the command)

```

### File Permissions Help
The first part of the output for the `-l` flag gives you information about the file's current permissions. There are ten slots in the
permissions list. The first character in this list is related to file type, not permissions, so we'll ignore it for now. The next three
characters relate to the permissions that the file owner has, the next three relate to the permissions for group members, and the final
three characters specify what other users outside of your group can do with the file. We're going to concentrate on the three positions
that deal with your permissions (as the file owner).

![](fig/rwx_figure.svg){alt='Permissions breakdown'}

Here the three positions that relate to the file owner are `rw-`. The `r` means that you have permission to read the file, the `w`
indicates that you have permission to write to (i.e. make changes to) the file, and the third position is a `-`, indicating that you
don't have permission to carry out the ability encoded by that space (this is the space where `x` or executable ability is stored, we'll
talk more about this later).

### EXERCISE 5.2
Change the permissions on all of your backup files to be write-protected.

```
Already did it

chmod -w *backup.fastq when in the backup directory

Also did the same command but with +w to add them all back and remove them again to double check

Before: 
-rw-r--r--. 1 gjb1039 domain users 47552 Feb 20 15:46 SRR097977_backup.fastq
-rw-r--r--. 1 gjb1039 domain users 43332 Feb 20 15:47 SRR098026_backup.fastq

After:
-r--r--r--. 1 gjb1039 domain users 47552 Feb 20 15:46 SRR097977_backup.fastq
-r--r--r--. 1 gjb1039 domain users 43332 Feb 20 15:47 SRR098026_backup.fastq

For chmod, you can put ugo options before the +/-rwx option to change for user group and others

```

How do you know they are write protected?
A:

No w in the permissions line in the space for user priviledges. Only seeing r's means that there is only read protections for user, group and others. Also no d at the start as they are files, not directories. Also no x in the permissions line means no one has execute priviledges

### EXERCISE 5.3: CONDA ENVIRONMENTS AND PROGRAMS
After loading a conda environment, where is the program 'fastqc' stored?

conda activate genomics: activates conda

conda deactivate: deactivates conda

fastqc *.fastq in untrimmed_fastq ran the fastqc, downloaded and openned the files

```

Stored in /home/share/anaconda/envs/genomics/bin/fastqc

Also unzipped all the fastqc .zip files we had that were zipped into a new directory

unzip [file name] to unzip files

```

### Explore the fastqc output. Which samples failed at least one of FastQC’s quality tests? What test(s) did those samples fail?


:::::::::::::::::::::::::::::::::::::::: keypoints
- Use `which` for commands/programs to see where they are installed
- You can view file permissions using `ls -l` and change permissions using `chmod`.
- The `history` command and the up arrow on your keyboard can be used to repeat recently used commands.
- Explain what a conda environment is, and how to activate and deactivate it

::::::::::::::::::::::::::::::::::::::::::::::::::