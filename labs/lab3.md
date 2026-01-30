# Lab3 - 2/16/24

## Pre-lab

1. Open up vscode
2. Control + shift + 'p' to open command prompt (command + shift + p on apple)
3. Start typing 'Connect to...' and the 'Connect current window to host' menu item will pop up. Select it
4. If asked, connect to ron.sr.edu host
5. Enter your RON username if prompted
6. Enter your RON password when prompted
7. You should see an 'open folder' on the left. Click it. The command prompt will have something like ```/home/unhAW/jtmiller/```. Click 'ok' open your home directory. If you saved a lab notebook to RON, you should see it on the left in a list of files. Click on it to open it. 
8. Next, we need to clone your gen711-811 github repo that you forked. Skip this step if you have done this already. If not, paste it into your lab notebook with <YOURGITHUBUSERNAME> replaced with your  username 
```
cd $HOME
git clone https://github.com/<YOURGITHUBUSERNAME>/gen711-811.git
```
9. Finally, we need to pull the latest updates to this repo. Run these commands:
```
cd gen711-811
git remote add upstream https://github.com/jthmiller/gen711-811.git
git fetch upstream
git merge upstream/master master
cd ~
```

### This might be the best option

1. Ensure all your local changes are committed to your current branch.
- Save all your vscode additions, and commit them. 
2. Fetch the latest updates from the remote:
```git fetch origin```
3. Rebase your changes onto the updated remote branch
```git rebase origin/main```
4. Resolve any conflicts: If conflicts arise during the rebase, Git will pause the process and prompt you to resolve them. After editing the files to resolve the conflicts, use:
```
git add .
git rebase --continue
```
## Lab Exercises (put these answers into your lab notebooks)

#### 3a  "3 ways to change directories to HOME from untrimmed_fastq"
1.
2.
3.

#### 3b. How many programs in /bin 
1. Do each of the following tasks from your current directory using a single ls command for each:
    - List all of the files in /Applications that start with the letter ‘c’.
    - List all of the files in /Applications that contain the letter ‘a’.
    - List all of the files in /Applications that end with the letter ‘o’.
    - Bonus: List all of the files in /Applications that contain the letter ‘a’ or the letter ‘c’.

Start with the letter c ____
Start with the letter a ____
Start with the letter o ____
Contain the letter ‘a’ or the letter ‘c’ ____

#### Find the line number in your history for the command that listed all the .fastq files using the absolute path. Paste the command that you used to do this below.
1.