# Lab3 - 2/6/26

# MY OWN NOTES SECTION

pwd : print working directory

directory : similar to a folder, things that contains other things like folders or files

ls : list, shows everything that is in the directory/folder you are currently in

cd : goes towards a chosen directory

cd ../ : steps back one directory, each "../" adds one step back

clear : just clears the terminal screen

ls ' : if you do this just put "'" to end it

Ctrl + C : cancels what you are doing/the current running command

Tab Complete : if you hit tab it will auto complete what you have typed, click it twice and it will show all the options that the autocomplete has

ls -F : lists but also tells you more data, "/" on names means they are directories you can enter into

man ls : manual list, tells you what options you have

ls -lrth : list with a bunch of extra metadata info like when and who made what along with permissions

head : shows you the header of the chosen file, sneak peek without fully opening it

cat : prints the whole to the screen

conda : environment manager, doubt I will need this info now but I will write it down anyways

cd ~ : goes back to base user page, can also do cd $HOME

relative paths : cd whatever is the path relative to where you are

absolute paths : pwd which starts at the start of the computer and takes the literal step by step path to wherever you are trying to go and traces it out

rm : deletes anything at RON you haven't pushed to GitHub

rm -fR : removes directory and everything in it

echo : evaluate a variable

history : shows command history 

grep : search command for within a file (Global Regular Expression Print), put the search query in '' and then the location after. Put ^ before your query inside the '' to search at the beginning of each line. Put > at the end followed by a file name to create a new file with what you searched

ls *fastq : lists everything that has fastq on the end of it, doesn't need to be fastq just whatever and you can put stuff before the * as well, * just means "whatever you can put here" 

"|" : pipes the output of a first command into the input of a second command

wc -l : word count, counts the number of lines in a given output

wc : word count basic, line, word and characters in order

ls /bin/c* | wc -l : takes all of the files from bin that start with c and then counts them 

ls /bin/ | grep '^c' | wc -l : lists bin, greps that search to look for starting c, word counts that output and gives you the line count

less file-c-prog : gives you a scrollable list of the files that starts with c in whatever director you are in

Add text here

## Before lab begins
1. Open up vscode
2. Control + shift + 'p' to open command prompt (command + shift + p on apple)
3. Start typing 'Connect to...' and the 'Connect current window to host' menu item will pop up. Select it
4. If asked, connect to 'ron.sr.edu host'
5. Enter your RON username if prompted
6. Enter your RON password when prompted
7. Go to 'File --> Open folder'
8. Select your 'gen711-811' directory
9. If you haven't done so already, save your workspace to this directory (File --> save directory as --> enter)
10. Take your notes in 'Markdown' format. See the readme.txt for taking notes for this lab below. 

# Part 1 (lab 3)
### Questions:
- What is a command shell and why would I use one?

let's us navigate our files easily

- How can I move around on my RON?

cd, ls, pwd are all useful for moving around

- How can I see what files and directories I have?

ls, ls -F for more info

- How can I specify the location of a file or directory on my computer?

pwd is the easiest way to do it, echo also maybe

### Objectives:
- Describe key reasons for learning shell.
- Navigate your file system using the command line.
- Access and read help files for bash programs and use help files to identify useful command options.
- Demonstrate the use of tab completion, and explain its advantages.

## The key points here are:
- The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI.
- Useful commands for navigating your file system include: ls, pwd, and cd.
- Most commands take options (flags) which begin with a -.
- Tab completion can reduce errors from mistyping and make work more efficient in the shell.

# Navigating Files and Directories
- How can I perform operations on files outside of my working directory?
- What are some navigational shortcuts I can use to make my work more efficient?

# Part 2 (lab 3)
## Objectives:
- Use a single command to navigate multiple steps in your directory structure, including moving backwards (one level up).
- Perform operations on files in directories outside your working directory.
- Work with hidden directories and hidden files.
- Interconvert between absolute and relative paths.
- Employ navigational shortcuts to move around your file system.

## More navigation
- We got an idea for moving around using cd and the name of the folder to move into. 
- But how to we go back out? We dont see the folder we are in.
- We have a special command to tell the computer to move us back or up one directory level.

### Your Notes Here: 
Seperate notes by an empty line, or they'll get pasted together

- Using a dash is helpful for lists
1. And numbers for lists

The pound sign is used for 'sections'. A single pound (or hashtag) in front of a word makes it appear bigger/bold to show a new section. See below

# My Notes:

To change directories, use 'cd' and then hit tab two times to see directories in my current directory





### Complete the questions below when intrstructed. Push the changes to this document to recive credit for attending the lab

#### 1. What are 3 ways to change directories to your home directory from the  untrimmed_fastq directory?
1. cd $HOME, takes you straight to home, same as cd ~
2. cd ~ 
3. cd ../ + however many ../ you need to get back (can figure it out with pwd in your current directory) 
4. cd /home/users/gjb1039/ uses the absolute path

#### 2. How many programs in /bin 
2. Do each of the following tasks from your current directory using a single ls command for each:
    - List all of the files in /bin that start with the letter ‘c’.

ls c*

    - List all of the files in /bin that contain the letter ‘a’.

ls c

    - List all of the files in /bin that end with the letter ‘o’.

ls *o

    - Bonus: List all of the files in /bin that contain the letter ‘a’ or the letter ‘c’.

ls 

#### Answers here
Start with the letter c 

ls c*

Start with the letter a 

ls a*

Start with the letter o 

ls o*

Contain the letter ‘a’ or the letter ‘c’ ____

We aren't getting to this today I think 

#### What command/commands would you use to find the line number in your history for the command that listed all the '.fastq' files using the absolute path. Paste your answer below.

history | grep '*fastq' 

it was line 100 for me in my history

we didn't do the absolute path part, so with the absolute path it would be line 134 in my history after doing the "ls /home/users/gjb1039/gen711-811/shell_data/untrimmed_fastq/*fastq" command first

asfg