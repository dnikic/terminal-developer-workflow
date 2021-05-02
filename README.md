# terminal-developer-workflow
## About
Vim, git, top, grep, find, jobs are all standard bash tools available even in the most minimal server installs (tty) and provide a environment suitable for software development.

## Short concept

```
Make executable script and a file for dumping its logs instead of executing commands directly in terminal.
touch ~/runterm.sh ~/logterm.log ; chmod +x ~/runterm.sh
Open multiple files in vim (as buffers) 
vim ~/runterm.sh ~/logterm.log
Execute comamands from it like 
:! ~/runterm.sh > ~/logterm.log &
list opened files in vim
:ls
Switch to log file (tab to autocomplete)
:b term.log
Refresh opened file 
:e
Save vim session
:mksession! ~/termvim.ses
Close all vim windows
:qa
Open other file in buffer
:e ~/other.txt
Empty the log file
: > logterm.log

You can relace > with >> if you want to append the output log file and not overwrite it when writing the output of runterm.sh.
```

```
Use git for managing changes and cooperative developement.
Use jobs to switch process in the same way as window minimizing.
Use top to monitor and manage system resource consumption and profiel or kill an running app.
Use w3m as a web browser.
Use vim sessions, buffers, windows  as a standard ide.
Set comamnds to you standard .vimrc so that you configure syntax highlights, tabs to spaces and more.
Manage a server using ssh.
```

## Vim (simple but versatile usage)

```
Vim working with multiple files

To see a list of current buffers, I use:
:ls
To open a new file in buffer I use
:e ~/log.txt
To switch between all open files, I use
:b myfile
Close file (delete buffer)
:bd
Split open a new split wondow where you can open a buffer=file
:sp and :vsp 
Ctrl-W w to switch between open windows (or Ctrl-W hjkl)
Ctrl-W c or :q to close the current window
Close window 
:q
Close all windows
:qa

You can save and open sessions in vim
(a session is a config of your opened fules im buffers and windows)
:mksession! ~/termvim.ses
vim -S ~/today.ses
:source ~/today.ses

Note: if you want all files to go to the same instance of Vim, start Vim with the --remote-silent option.

Open multiple files as split windows
horizontal or vertical
vim -O file1.txt file2.txt
vim -o file1.txt file2.txt
```



```
Vim text editing

Manipualtion and commands mode
esc
Writing mode 
a,i,A,I
a append with text
i insert text
I start of line (or home key)
A end of line (or end key)
Move cursor
h,l per charcter, w,b per word
j,k down and up
arrows also work
Select text
v and movement or V for whole line (also highligts it)
Copy(yank) and paste text 
(works also between buffers)
y and p
/ simple search, use n for next and N for previous
open the search history
q/ 
paste the yanked text on the command line and search
p Enter 
:%s/oldText/newText  replace all oldText with newtext
:s/oldText/newText  replace all oldText with newtext in curent line
% jump to matching bracket (shift +5)
u  to undo (steb back)
:redo enter or ctrl r  to redo
:q! exit without saving
:w vimtest.txt save file (write)
:13 jump to line 13
x dw dd cut commands (used for deleting character, word or line)
. repeats last command
autocomplete
ctrl+n
Select all (select down a large nuber of lines)
v99999
Run bash terminal pwd command
:! pwd
Run bash ping terminal command in background
:! ping google.com &

Indent text
>>
Unindent text
<<
```



```
Vim multiline editing

Vim visual block 
ctrl v
go up or down with j k
:normal I someprefix
adds the prefix to all lines
Remove last 3 character of 4 lines
ctrl v jjjj
:normal $jjxxx

Vim macro
qa Record macro to a register
Do something
q Stop recording
@a Apply macro tu curent line
15@a Apply macro to 15 lines below
```

## Very usefull usefull bash commands
```
Find files with word "gesture" inside in subfolders of curent folder
(usefull for finding function definitions)
(r search subfolders, i case insensitive,  n show line number of word in file)
grep -rin 'gesture' .
Pipe multiple grep commands
(List in subfolders files that case insensitively contain img, an extract lines from that list that dont have Binar in them
grep -ri img .| grep -v Binar
Filter filenames with .js using grep and find
(in subfokders)
find . | grep .js
```
```
~/Downloads means /home/user/Downloads
Change directory 
cd somefolder
Go up directory
cd ../
(double upp ../../)
Remove file
rm filename.txt
Execute file 
./filename.sh
List visible and hidden files
ls -a
Make file executable
chmod +x /path/to/your/file.sh
Rename file
mv oldname.txt newname.txt
Move file (or copy)
mv furstpath/myfile.txt newpath/myfile.txt
(use cp to copy instead of move)

Find where your program is being ran from
which myProgram
```

## Vim setup

```
Convert tabs to sapces
:retab  
Show line numbers
: set number 
Show title of opened file
:set title
Syntax hightlight colors
:syntax on
```

Add tabstospaces and line numbers

```
vim ~/.vimrc 
```
Add these lines:
```
" tabstop:          Width of tab character
" softtabstop:      Fine tunes the amount of white space to be added
" shiftwidth        Determines the amount of whitespace to add in normal mode
" expandtab:        When this option is enabled, vi will use spaces instead of tabs
set tabstop     =4
set softtabstop =4
set shiftwidth  =4
set expandtab
set number
set title
syntax on
```

## tty tips 

```
(managing executed scripts as jobs in single terminal)
Send output to file
ping google.com > myLog.log
Refresh oepned log in vim with
:e
Execute process in background  
(if you add nohup before it can not read input but it will survive if you close the terminal)
ping google.com > myLog.log &
Find background process
jobs
Send process to background 
bg%1
Send process to foreground by process job id
fg %1
Stop/pause curent process 
(it will be available in jobs to open woth fg)
ctrl z 
Kill curently opened process
ctrl c
kill job
kill 1%
Suspend vim to background and return to it
ctrl+z or :sus
Afterwards in bash
fg

W3m terminal web browser
w3m google.com
```

## Top tips (terminal system monitor)

```
open top with top comamnd
Press q to quit
Press h for help
Press k for kill and write PID and enter to kill.
Press Shift L for search (look for)
Up and down arrows to go through list
CPU and memory ussage is presented in %
Press m for diferent graphical representaion of used memory
Press Shift+p sort processes by CPU usage
Press Shift+m sort processes by memory usage
Press Shift+r reverse sort order
Press d and write refresh interval in seconds
Additional
https://vitux.com/how-to-use-the-ubuntu-linux-top-command/
```

## Git command line

Look at git command outputs, they show you options on what to do next.
For example git status explains how to stage, unstage and reset file changes.

```
Basic
Create repository
git init 
Clone a repository
git clone some/repsoitory/name.git
Show status of locla repository
git status
Stage what will be committed
git add myfile.txt 
Discard changes in working directory
git restore myfile.txt 
of
git checkout -- myfile.txt
Unstage a file
git restore --staged myfile.txt 
or
git rm --cached myfile.txt
Commit staged changes
git commit -m 'First commit message"
Push commit from lcoal repository to remote repository
git push
Show commits
git log
Change code to some commit
git checkout somecommit
```
```
Branches
Create a branch
git checkout -b "mybranch"
Cange to some branch
git chechout branchname
Merge branch to curent branch
git merge somebranch
Stop merge process
git merge --abort
```

```
View differencess
Show curent unstaged changes in all files
git diff
Show curent changes in single file
git diff filename.txt
Compare code of the checked out branch to branch_2
git diff ..branch_2
List commits on mybranch created from develop
git log develop..mybranch
Compare to origin=last pulled state of file
git dif origin/branchname/path/to/file.txt

Check  who & when wrote witch line in a file
git blame path/to/file.txt
```
```
Soft reeset
Remove commit but kep changes from that commit as staged files.
git reset --soft HEAD~1

Git stash
Move and save staged curent changes to a stash
git stash push -m "message"
Get list of shashes to get your stashes index number
git stash list 
Retrieve changees from stash for example 5
git stash apply --index 5

Change commit history
Interactive rebase
git rebase -i HEAD~4
A text editor will open and there you may change pick to reword witch will let you rename a commit. Changing pick to d will drop (delete) that commit from commit history. All commits where pick is repalced with squash will be merged int one.
After performing rebase you need to force push changes
git push --force

Rebase workflow
(mybranch was created from master)
git checkout master
git pull
git checkout mybranch
git rebase master
#Fix possible merge conflicts marked in you files, save files, stage them with git add somefile.txt and then continue the rebase procedure
git rebase --continue
When an output stating no rebase in progress is present, the rebase is finsihed.
Use git status to check repo and files during the rebase procedure.
git push --force
To sto the rebase procedure use 
git rebase --abort
Sometimes you maywant to put newly pulled changes below you local commits
git pull --rebase

Reset to remote
checkout mybranch
git reset origin/mybranch
git restore .
git pull


Transfer commits from one branch to another
on some branch there are commits X,Y Z that i want on mybranch
git checkout mybranch
git cherry-pick SHA-COMMIT-X
git cherry-pick SHA-COMMIT-Y
git cherry-pick SHA-COMMIT-Z
```

```
Git over ssh
 ssh-keygen -t rsa -b 4096
 You can leave blank on all
 cat ~/.ssh/id_rsa.pub 
 Coppy to bitbucket on https://bitbucket.org/account/settings/ssh-keys/
Gto to clone and and switch to ssh and get new link to ssh instaed of https
 Switch your local repo to ssh
 git remote set-url origin <copy-link-here>
 Example 
 git remote set-url origin git@bitbucket.org:someuser/test.git
 Checkif you can acces the repo
 git fetch
```



## Connect to another computer using SSH

```
Start ssh server on host (computer to witch you want to connect)
sudo apt update
sudo apt install openssh-server
sudo systemctl status ssh
sudo ufw allow ssh
Check weather ssh server is runing
sudo systemctl status ssh
Get ip adress of host 
ip a
Connect from client to host using ssh
Default port is 22 but you may specify another like 4444
ssh someuseronhost@hostipadress
ssh -P 4444 cooladmin@192.168.0.24
Copy files from host to client using SCP
scp -P 4444 cooladmin@192.168.0.24:/home/cooladmin/Downloads/somefile.txt ~/Downloads/
Copy files from client to host using SCP
scp -P 4444 ~/Downloads/somefile.txt cooladmin@192.168.0.24:/home/cooladmin/Downloads/ 

Grant all users right to folder and files within
(a is for all)
sudo -R chmod a+rwx 

Tree comand alternative for servers
find . | sed -e "s/[^-][^\/]*\// |/g" -e "s/|\([^ ]\)/|-\1/"
```

## Mouse keys

```
Use numpad as mouse
On ubuntu enable mouse keys, and change sensitivity 
sudo apt install xkbset
watch -n 1  xkbset ma 60 10 10 5 10
Under Universaal access enable mouse keys or Hold Shift and press Num-Lock to enable keyboard mouse emulation.
```



