# terminal-developer-workflow
## About
Vim, git, top, grep, find, jobs are all standard bash tools available even in the most minimal server installs (tty) and provide a environment suitable for software development.


```
Use git for managing changes and cooperative developement.
Use jobs to switch process in the same way as window minimizing.
Use top to monitor and manage system resource consumption and profiel or kill an running app.
Use w3m as a web browser.
Use vim sessions, buffers, windows  as a standard ide.
Set comamnds to you standard .vimrc so that you configure syntax highlights, tabs to spaces and more.
Manage a server using ssh.
```

```
If the documentation or code completion is faulty or insufficient you can download the source code of the library and just search for a function deffinition or data type and see its parameters.
```


## Managing script log files

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
Refresh opened file and show its path
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
You can pipe the output directly into vim for copying and pasting into toher opened vim instances (or into bash command line if bash is se to vi mode) with:
pwd | vi -
If you want to watch the bash output, and meanwhile write it to a file in background, pipe the output to the tee command: 
./~/runterm.sh | tee ~/work/localCore.log

If you dont want to write outputs to disk, but instead to a vim buffer in ram read below the "Vim executing commands and viewing outputs" section.
```




## Vim usage

```
Vim simple file browsing

To open the file browser use:
vim . 
or from within vim use :
:E
To exit file browser
:Rexplore or :bd like closing any other oepned buffer
Show opened files
: ls
Switch to some opened file
:b partOFName and press tab for atutocomplete and hit enter
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
h,l per charcter, e,b per word
j,k down and up
arrows also work
Select text
v and movement or V for whole line (also highligts it)
Copy(yank) and paste text 
(works also between buffers)
y and p or P
/ simple search, use n for next and N for previous
q/ Open the search history (paste the yanked text using p on the command line and search with enter)
:%s/oldText/newText  replace all oldText with newtext
:s/oldText/newText  replace all oldText with newtext in curent line
% jump to matching bracket (shift +5)
u  to undo (steb back)
:redo enter or ctrl r  to redo
:q! exit without saving
:w vimtest.txt save file (write)
:13 jump to line 13
x de dd cut commands (used for deleting character, word or line)
. repeats last command
ctrl+n Autocomplete what i am writing
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

Replace word in vim
Select and coppy word
vey
Select and paste over word
vep

```

```
Vim executing commands and viewing outputs

Get output of bash command

Open commands history buffer
q:
Enter insert mode with i or paste with p
Add ! t othe begining of bash command to make it executable
! ls
You may navigate rows up and down with jk or arrows to chose previously executed commands
Pres enter to execute command in the curenty row
if you dont want to execute a command press enter on an empty command row or press Ctrc C
To pipe thecommands output to current buffer use r! instead of !
r! ls


Ge output of vim command 

Get currently oepend buffer path (read output of command f)
call feedkeys("i".execute("f"))

```

```
Multiple search highlights inside same file

#Show available colors (q to exit colors list) Highlight all "Ready finished" in file as Error color and highlight all MainDoorOpened with Todo color, then clear all colors 
:highlight
Match with regex
match Error /Ready\sfinished/
Match with string
match Error 'Ready finished'
Second color
2match Todo /MainDoorOpened/
match none
2match none
```


```
Vim multiline editing

Delete all line where "Bianry File" is present
g/Binary File/d


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



```
Vim more in depth working with multiple files

To see a list of currently opened buffers and their numbers:
:ls
To open a new file in buffer
:e ~/log.txt
To switch between all open files, use name or buffer number
:b myfile or :b 2 
Close file (delete buffer)
:bd
Split open a new split wondow where you can open a buffer=file
:sp and :vsp 
Ctrl-w w to switch between open windows (or Ctrl-w hjkl)
Ctrl-w c or :q to close the current window
Close window 
:q
Close all windows
:qa

You can save and open sessions in vim
(a session is a config of your opened fules im buffers and windows)
:mksession! ~/termvim.ses
vim -S ~/today.ses
:source ~/today.ses


Open multiple files as split windows
horizontal or vertical
vim -O file1.txt file2.txt
vim -o file1.txt file2.txt


Set size of current Vim window
:resize 40
:vertical resize 40
Add +5 or -5 instead of 40 to increment the current size by 5 instead of setting it to 40.
Or use mouse to drag the split edge if mouse=a enabled
```


```
Simply search for text in files (vimgrep)
q: paste yanked word with p and use
:vimgrep /someword/ ./**/*.txt
ctrl w w to switch windows 
ender on select found word in file
or use :cnext and :cprev

Fuzzy open a file (native no addons or config)
:find ./**/test* 
press tab tuntill you find what you want



Searching for text inside files using Vim (vim + grep = VSCode+ctrl+shift+f )

Search recursivley in files for 'some text'
:grep -rI 'some text' .
Press enter
Open the resaults with previews window
:copen
Use arrows or jk to navigate up and down and enter to open a file as buffer
You can make the opened quicklist editable with command
:set modifiable
To remove all lines WITH "Binary File" text use command
:g/Binary File/d
To remove all lines WITHOUT "Binary File" text use command
:g!/Binary File/d
Switch between opened buffer as window and resaults window
Control ww
Close current window
:q
Opened files in the resauls window will remain as buffers
Show current buffers and their numbers
:ls
Delete buffer 5 and buffer 51
:bd 5 51

Find a definition with vim + grep
grep -rI 'void ActivateBackOffice(' .


```

## Vim developer setup

Open vimrc
```
On Linux bash
vim ~/.vimrc 
On Windows bash
vim /c/Users/d.nikic/.vimrc
```

Add these lines:
``` 
set tabstop     =4 " Width of tab character
set softtabstop =4 "Fine tunes the amount of white space to be added
set shiftwidth  =4 "Determines the amount of whitespace to add in normal mode
set expandtab "When this option is enabled, vi will use spaces instead of tabs
set encoding=utf-8
set ve+=onemore "Can navigate one character after last in row
set linebreak
set number
set title
set cursorline "Highlight current line and use hi defined styling for the line and line number
set hidden "Enables you to switch buffer without saving changes to disk
syntax on
set mouse=a
set belloff=all
"set clipboard=unnamedplus " Use system keyboard, to install: sudo apt install vim-gtk
"More common search behaviour
set hlsearch
set ignorecase
set incsearch
"Fuzzy file search like in VSCode activated by Ctrl p, cycle opetions using tab key
nnoremap <C-p> :find ./**/*
"Fuzzy CTRL SHIF F like in  VSCode, aka vimgrep
nnoremap <C-S-f> :vimgrep /someword/ ./**/*.txt
" Make d delete and not cut, sue x for cut
nnoremap d "_d
nnoremap D "_D
vnoremap d "_d
" Make vim use 256-color mode
set t_Co=256
" Section used for styling
hi CursorLine cterm=NONE ctermbg=0
hi CursorLineNr cterm=bold ctermbg=0
hi StatusLine ctermbg=none cterm=bold
hi StatusLineNC ctermbg=0 cterm=NONE
hi VertSplit cterm=bold
set fillchars+=vert:.
" Plugins
"call plug#begin()
"Plug 'sheerun/vim-polyglot'
"Plug 'airblade/vim-gitgutter', {'on': 'GitGutterEnable'}
"call plug#end()
" After plugins
set whichwrap+=<,>,h,l,[,] " Common wrapping (go to next line when going right on line end)
```


Lightweight usefull Vim plugins
```
Install Vim Plug plugin manager
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

At the end of ~/.vim add:
set nocompatible
call plug#begin()
Plug 'sheerun/vim-polyglot'
Plug 'airblade/vim-gitgutter', {'on': 'GitGutterEnable'}
call plug#end()

After runing Vim activate plugins
:PlugInstall

To set dart language syntax from an yet unsave file use:
:set syntax=dart

To see curently set syntax highlight:
:setlocal syntax?

Language servers like coc plugin imapct performance, it's faster to grep in the docs and analize compilation errors.

Change colorscheme in Vim
mkdir /home/dnikic/.vim/colors
On website vimcolorschemes.com find your prefered color scheme, and add its somethemename.vim file to /home/dnikic/.vim/colors
Opne vim or add to vimrd
:colors somethemename


```

```
Fuzzy file search like in VSCode 
(Availabe after setting up basrc command mentioned before)
Activate by Ctrl p, cycle opetions using tab key
```

```
Convert tabs to sapces in file using tabs
:retab  
```

Bash in Vi mode
```
(When in bash terminal press Esc and v to enter full vim for more detail editing of current command)
(Enables you to select and copy from and to bash terminal line)

Add to ~/.bashrc
set -o vi
Then run 
source ~/.bashrc
```


## Common usefull bash commands

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


```
grep tips (searching for files or their content) 

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
Show found init.setup text and 4 lines before and after it (usefull for previewing code definitions)
grep -B4 -A4 -rin 'init.setup'
Outputs of grep are formated as log files and can be highlighted in Vim with command
:set syntax=log
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
Show changes in files through commit history
git log -p
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
Delete local branches that were previously deleted on remote
git remote prune origin
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

Read main.c as it was 4 commits ago using less text reader.
git show HEAD~4:src/main.c

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

Undo an action (a rebase for example)
git reflog 
Compy the code of the action for example 1d69c86
git reset 1d69c86


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

```
Set git creditentials
(They will show next to your commit and should match ones in your github account)
git config --global user.email "danilonikic4@gmail.com"
git config --global user.name "Danilo Nikic"
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
sudo chmod -R a+rwx 

Print a tree structure of subfolders and their files
tree
Alternative for servers where tree is not installed
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



