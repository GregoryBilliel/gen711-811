---
title: Working with Files and Directories
teaching: 30
exercises: 15
---
# Lab4 - 2/13/26

# MY NOTES

pwd gives the absolute path for the directory/folder/file you are currently in

cd with nothing after it takes to the home directory, also cd ~ or cd $HOME

cd ~/[tab] tells you what is in your home, easy way to navigate around

cd ../ is a backspace, can chain them together

ls -a : lists all the files, including hidden ones, could also do ls --all

ls .* : lists just all the hidden files and tells what is inside them

ls -laF : lists the files, user and permissions as well as when it was created

drwxrwxrwx : permissions

d = directory

r = read

w = write

execute = x

the order of the rwx trios indicates who has permissions, first three are for the owner I remember that much at least

second gruop in for group 

last gruop is for others

ls /usr/bin/c* | wc -l : piped command, doubt you'll need this again but fuck it here it is

tail : looks at the end of a file

less -S : shows a window of the file in an easy way



::::::::::::::::::::::::::::::::::::::: objectives

- View, search within, copy, move, and rename files. Create new directories.
- Use wildcards (`*`) to perform operations on multiple files.
- Make a file read only.
- Use the `history` command to view and repeat recently used commands.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I view and search file contents?

ls command, pretty simple

- How can I create, copy and delete files and directories?

touch : makes file, put name after with .txt 

mkdir : makes directory, put name after

cp : copies, put source file then destination next, can put a directory path as well

cp -r: recursive copy of everything that is in a directory

rm : removes a file

rmdir : removes a directory

rm -r :removes a nonempty directory 

- How can I control who has permission to modify a file?
- How can I repeat recently used commands?

::::::::::::::::::::::::::::::::::::::::::::::::::

### EXERCISE 1: NAVIGATION PRACTICE
Navigate to your untrimmed_fastq directory in one command

cd gen711-811/shell_data/untrimmed_fastq/

### EXERCISE 2: WILDCARDS
What would the output look like if the wildcard could *not* be matched? Compare the outputs

it just says it could not find the file or directory

### EXERCISE 3: NAVIGATING PRACTICE
Navigate to your home directory. From there, list the contents of the untrimmed_fastq directory.

ls gen711-811/shell_data/untrimmed_fastq/

:::::::::::::::::::::::::::::::::::::::  challenge

## Relative path resolution

Using the filesystem diagram below, if `pwd` displays `/Users/thing`,
what will `ls ../backup` display?

1. `../backup: No such file or directory`
2. `2012-12-01 2013-01-08 2013-01-27`
3. `2012-12-01/ 2013-01-08/ 2013-01-27/`
4. `original pnas_final pnas_sub`

![](fig/filesystem-challenge.svg){alt='File System for Challenge Questions'}

:::::::::::::::  solution

## Solution

1. No: there *is* a directory `backup` in `/Users`.
2. No: this is the content of `Users/thing/backup`,
  but with `..` we asked for one level further up.
3. No: see previous explanation.
  Also, we did not specify `-F` to display `/` at the end of the directory names.
4. Yes: `../backup` refers to `/Users/backup`.

Number 4 is the example, the ls command ../ goes back into the users folder and then lists the contents of the right backup directory 

:::::::::::::::::::::::::


### EXERCISE 4: FINDING HIDDEN DIRECTORIES
First navigate to the shell_data directory. There is a hidden directory within this directory. Explore the options for ls to find out how to see hidden directories. List the contents of the directory and identify the name of the text file in that directory.

Hint: hidden files and folders in Unix start with ., for example .my_hidden_directory

What is the hidden file name in the hidden directory?

Already did this, it was a hidden file that had some text in it, found using ls -a

### EXERCISE 5: HISTORY
Find the line number in your history for the command that listed all the .sh files in /usr/bin. Rerun that command.

Go into history, find the number of the desired command, then put ![#] into the terminal

could also pipe a history command into a grep command to search through your history easily

ls /usr/bin/*.sh was line number 231 in my history, reran using !231

### EXERCISE 6: FILE CONTENTS
Print out the contents of the ~/shell_data/untrimmed_fastq/SRR097977.fastq file. What is the last line of the file?

cat prints out the whole file so: 

cat ~/gen711-811/shell_data/untrimmed_fastq/*977.fastq

last file line: C:CCC::CCCCCCCC<8?6A:C28C<608'&&&,'$

can you do grep [query] [file name] to find the amount of times it is listed. Add a pipe with a wc -l to get an exact number of the lines that have it

tail -n3 : only gives last 3 lines of a tail

### EXERCISE 7: PATHS
From your home directory, and without changing directories, use one short command to print the contents of all of the files in the ~/shell_data/untrimmed_fastq directory.

cat ~/gen711-811/shell_data/untrimmed_fastq/*

### EXERCISE 8: LESS
What are the next three nucleotides (characters) after the first instance of the sequence quoted above?

we used less in class, we didnt use it all much 

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
talk more about this later.

### EXERCISE 9
Starting in the shell_data/untrimmed_fastq/ directory, do the following:

Make sure that you have deleted your backup directory and all files it contains.
Create a backup of each of your FASTQ files using cp. (Note: You’ll need to do this individually for each of the two FASTQ files. We haven’t learned yet how to do this with a wildcard.)
Use a wildcard to move all of your backup files to a new backup directory.
Change the permissions on all of your backup files to be write-protected.

mv : moves files to other places

mv *backup.fastq backup/

### EXERCISE 10: PROGRAMS
After loading a conda environment, where is the program 'fastqc' stored?



:::::::::::::::::::::::::::::::::::::::: keypoints

- You can view file contents using `less`, `cat`, `head` or `tail`.
- The commands `cp`, `mv`, and `mkdir` are useful for manipulating existing files and creating new directories.
- You can view file permissions using `ls -l` and change permissions using `chmod`.
- The `history` command and the up arrow on your keyboard can be used to repeat recently used commands.

::::::::::::::::::::::::::::::::::::::::::::::::::