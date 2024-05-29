# LECTURE NOTES: The Unix Shell

**Instructor:** *Manuel G. Garcia*

**Last update:** *29-05-2024*

**Presentation:** *[Intro to Unix-shell](https://docs.google.com/presentation/d/1ySjg6TLzC63DgO3j9M8Ynx9QrUijeFDQ/edit?usp=sharing&ouid=105684743155471216616&rtpof=true&sd=true)*

**Exercises:** *[Unix-shell exercies with answers](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)*

These are lecture notes for the beginner-level of one of the lessons of the [Software Carpentry](https://swcarpentry.github.io/shell-novice/). These notes assume the use of [Git terminal for Windows](https://gitforwindows.org/).
The context and flow of this lesson have been addapted to better fit the audience.

## PREPARATION
The instructor sets up the [gitautopush](https://pypi.org/project/gitautopush/) and the command history on two terminals:


### Change where Bash history is stored

```shell
# create  file to storing the terminal history
touch <path-to-repo>/unix_shell
# modify .bashrc or .bash_profile and change HISTFILE
export HISTFILE=~/<path-to-repo>/unix_shell
# reload configuration to terminal 
source ~/.bash_history # or .bashrc
# start gitautopush
gitautopush <path-to-repo> --sleep 5
```

### Show history in split terminals

1. On main terminal:
```bash
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
$ tail -f ~/<path-to-repo>/unix_shell | nl -w 3
```

### Windows Terminal (Preview) [Keyboard shortcuts]
Useful shortcuts for the Windows Terminal (Preview) App on Windows 11.

| Action             | Shortcut                |
|--------------------|--------------------------|
|Split pane horizontally | Alt + Shift + `-`   | 
|Split pane vertically   | Alt + Shift + `+`   |
|Close a pane            | Ctrl+Shift + `w`     |
|Move pane focus         | Alt + `Arrow keys`   |
|Resize the focused pane | Alt+Shift + `Arrow keys` |

### Lesson Data

[Download the dataset](https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip) for this lesson before starting. 
 
------

## PART 1
### 0. INTRODUCTION [10 min]

> A Quick introduction to what a BASH terminal. What it is and what it is used for (Slides)

> Explain when and why CLIs are more useful than GUIs.

### 1. EXPLORING THE TERMINAL [10 min]

a. Open Bash terminal

b. Go to the home directory with **c**hange **d**irectory

> MacOS user should invoke a Bash terminal first: `bash`
 
 ```shell
    cd ~
 ```

c. Explain the Anatomy of the Terminal

> Explain the meanding of tilde `~` in a unix shell

> Explain the meaning of the  **prompt** `$`. Other symbols are possible. The prompt symbol is not part of a command.

> Explain the **text cursor**, symbols can be: a flashing block, underscore, a pipe, or other. 

| Symbol(s) | Name | Meaning |
|-----------|----------|----------|
| `$`       | prompt | Ready for a command
| `_`,  ` \|`, :white_square_button:  | text cursor | position where you're typing will appear|
| `user@host` |  | who and to which computer the CLI is connected to |
| `~/Desktop/workshop/` | path | current directory|

d. Basic command syntax
    
```shell
<command/program> [options] <arguments>
```

Example: listing the contents of a directory.

```shell
ls 
```

```shell
ls --help
```

### 2. EXPLORING DIRECTORIES [30 min]

#### The **p**resent **w**orking **d**irectory:

```shell
pwd
```

> Explain how different OS's represent a path to a directory differently. 

> Explain what a file system is and how files are organise, also explain the meaning of *root* directory (Slide x).

#### **l**i**s**ting content in a directory

```shell
ls
```

```shell
ls -F
```

> Explain: `/` a directory, `@` a link, `*` executable

```shell
ls -l
```

```shell
ls -lh
```

```shell
ls -a
```

```shell
ls -s
```

```shell
ls -S
```

> **l**ong option, **h**uman readable, **a**ll (including hidden files and directories), **s**ize of files and directories, **S**ort files and directories by size. Give examples while in `~/`

a. Listing order

```shell
ls -t
```

```shell
ls -tr
```

> Explain: alphabetically (default), by *t*ime (most recent modified), and in **r**everse order

b. **Clear**ing the terminal and accessing previous commands

```shell
clear
```

> Explain use of Up and Down arrow keys to 

d. Exploring the `shell-lesson-data`  directory

```shell
ls -F Desktop
```

```shell
ls -F Desktop/shell-lesson-data
```

> Explain **TAB** completion.

```shell
ls -R Desktop/shell-lesson-data
```

> Show content of subdirectories **R**ecursively.

###  **C**hanging **d**irectory

a. Change location into the `exercise-data` directory

```shell
cd Desktop
cd shell-lesson-data
cd exercise-data
```

> You can use `pwd` to confirm in which directory you are.

b. Changing directory backwards

```shell
cd shell-lesson-data
```

> this fails because `cd` only is aware of subdirectories in the current directory.

```shell
cd ../
```

> explain meaning of shortcuts: `..` and `.`

> Questions?

c. Changing directories using absolute paths

```shell
cd /Users/<your-user-name>/Desktop/shell-lesson-data/exercise-data
```

> Explain the use of shortcuts for navigating directories: `~/` (user-home directory), `cd` (no argument defaults to home directory), `-` location of previous directory

### 3. WORKING WITH FILES AND DIRECTORIES [40 min]

#### Creating directories

a. Move to `exercise-data/writing` directory and list its content:

```shell
cd shell-lesson-data/exercise-data/writing
ls -F
```

b. Create the *thesis* directory using the **m**a**k**e **dir**ectory command:

```shell
mkdir thesis
```

c. Create `project/data` and `project/results` directories and its **p**arents, in *./thesis/*

```shell
mkdir -p ./thesis/project/data
mkdir -p /thesis/project/results
```

> Explain what to avoid when naming directories, e.g., spaces, capitals, special characters other than `., -, _`

d. Creating files using a text Editor

```shell
cd thesis
nano draft.txt
```

> Explain importance of file extentions.

e. Creating files using `touch`

```shell
touch my-file.txt
```

### **M**o**v**ing, **c**o**p**ying and **r**e**m**oving files and directories

a. Go to `shell-lesson-data/exercise-data/writting`

b. Move `haiku.txt` to `./thesis`

```shell
mv thesis/haiky.txt thesis/quotes.txt
```

b. Move (rename) `draft.txt` to `quotes.txt`

```shell
mv thesis/draft.txt thesis/quotes.txt
```

> Explain `mv` also works for directories. Be careful `mv` may overwrite files, use `-i` to check.

c. **C**o**p**y `quotes.txt`

```shell
cp quotes.txt thesi/copy-quotes.txt
```

d. Copy a directory and its content

```shell 
cp -r thesis ./thesis_backup
```

e. Removing files and directories

```shell
rm quotes.txt
```

```shell
rm -r thesis_backup
```

> Explain, be careful with `rm`. Files will be permanently deleted. To check use `rm -i`. Explain `cp` and `rm` accept multiple arguments.

> Questions?

#### Using Wildcards

> Explanation: wildcards are used to enable pattern matching and they help to apply commands to multiple files and directories. Explain **\*** (zero or more characters), and **?** (any one character).

a. List files in `alkanes` directory

```shell
ls *t*ane.pdb
ls *t?ne.*
ls *t??ne.pdb
ls ethane.*
```

-----------------
## BREAK 
-----------------
## PART 2

### 4. EXERCISE [10 mins]

Breakout session 1: [Files & Directories](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)

### 5. PIPES AND FILTERS [21 min]

> Work on the directory `shell-lesson-data/exercise-data/alkanes`. The files with `.pdb` extension are from the *Protein Data Bank* (plain text, speficy the position of each atom in a molecule)

a. List the content of the directory

```shell
cd shell-lesson-data/exercise-data/alkanes
ls
```

b. Use the **w**ord **c**ount command to count the content of a file

```shell
wc cubane.pdb
```

> Meaning of output: number of *lines, words and characters*

c. Use `wc` and wildcards to count the countent of all files with `*.pdb` extension.

```shell
wc *.pdb
```
d. Show only the number of *lines*

```shell
wc -l *.pdb
```

> Other options: `m` for number of characters, `w` for number of words.

e. Try to use `wc -l` without arguments.

> command waits for input from the command line.  Use *CTL + C* to cancel the command

#### Which file contains the fewest lines?

> What we need to do to find an aswers using the CLI? Which steps? Ask participants to think
> We will explore some commands that can help us in finding an answer. 

a. Save command's output to a file

```shell
wc -l *.pdb > lengths.txt
ls # check file was created
cat lengths.txt # list the content of the file
```

> Cat dumps all the content on the screen. To display content in chunks, use the `less` command (`spacebar` for next page, `b` for back).

a. Ask participants to show the content of `shell-lesson-data/exercise-data/numbers.txt`

```shell
cat ../../numbers.txt
```

b. sort the content 

```shell
sort ../../numbers.txt # aphabetically
```

```shell
sort -n ../../numbers.txt # numerically
```

c. saving sorted list to a new file

```shell
sort -n  lengths.txt > sorted-lengths.txt
```

> Use `>` with caution it will rewrite files without warning, `>>` appends content to a file.

d. filtering output

```shell
head -n 1 sorted-lengths.txt
```

> Explain `-n <number>` and `head input `. And also the `tail` command.

```shell
tail -n 5 sorted-lengths.txt
```

#### Pipelines
They combine two or more commands. The `|` symbol take the output on one command as input for another command (Slide 11)

a. Sort and listing the first result

```shell
sort -n lengths.txt | head -n 1
```

b. We can combine the steps from the case above into pipelines.

```shell
# pipeline for counting and sorting
wc -l *.pdb | sort -n
```

```shell
# pipeline for counting, sourting and filtering
wc -l *.pdb | sort -n | head -n 1
```

> Questions?


### 6. EXERCISE [10 mins]

Breakout session 2: [Pipelines and Filters](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)

------------------

## PART 3

### 7. SHELL SCRIPTS & LOOPS [15 min]

> Scripts are list of commands (representing a program) and saved to a file. They are useful when we expect to repeat the same commands for different inputs. When we want to automate tasks.

a. Create a script to select lines 11-15 from the `octane.pdb` file

```shell
cd alkanes
nano middle.sh
```

```shell
# content for middle.sh

head -n 15 octane.pdb | tail -n 5
```

> use **CTRL + O** to save, and **CTRL + X** to exit the editor.

b. Run the script using BASH

```shell
bash middle.sh
```

### Passing arguments to a script

> We can define varialble in BASH 

a. Edit the  `middle.sh` script as follows.

```shell
head -n 15 "$1" | tail -n 5
```

> `$1`is a placeholder for a positional argument. A value must be passed when executing `middle.sh`. We use double quotes here to allow the use of spaces in the value for the argument.

> Save changes, and execute `middle.sh` again. Explain which advantages the new script has compared with the first version.

b. Define multiple arguments and add comments

```shell
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines

head -n "$2" "$1" | tail -n "$3"
```

 c. Run the script

```shell
# example 1
bash middle.sh pentane.pdb 15 5
# example 2
bash middle.sh pentane.pdb 20 5
```

> What if we want to allow  sorting many files wihout restricting the number of files. Explain use of `$@`to define a variale number of arguments.

a. Create a new script and include the following conent

```shell
nano sorted.sh

## content of script:

# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n

```

b. Run script for all `pdb` and `dat` files in 

```shell
bash sorted.sh *.pdb ../creatures/*.dat
```

### 8. EXERCISE [10 mins]

> Move location

Breakout session 3: [Shell Scripts](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)


------
## BREAK [15 min]
-----

### Looping [25 min]

> Explanation. Loops are a programming construct which allow us to repeat a  set of commands for each item in a list. Use pseudo-code to explain `for` loops.

> Use case. Suppose we want to print the classificaiton of each species in the files of the `/creatures` directory. The commands that are helpful in this case are `head -n 2` and then `tial -n 1`

a. move to `/creatures` directory

```shell
cd exercise-data/creatures
```

b. Create a shell script: `species.sh`, and  use a `for` loop to apply those commanad to all `.dat` files


```shell
for filename in basilisk.dat minotaur.dat unicorn.dat
do
    echo $filename
    head -n 2 $filename | tail -n 1
done
```

> Explain how to define variables, and that they can be invoke using `$variablename` or `${variablename}`. The later reduces ambiguity. 

c. Another case. If we want to modify all files in `/creatures` directory, but make a back-up firts. We can try to use wildcards for this

```shell
cp *.dat original-*.dat
```

> The above fails with `cp: target original-*.data is not a directory`. **cp** expects a directory when multiple files are passed as the first argument.

d. We can use a `for` loop instead, directly on the CLI.

```shell
for filename in *.dat
do
    cp $filename original-$filename
    echo $filename "was copied" 
done
```

> Explain how `echo` is useful to provide feedback on commands that do not produce standard output.

e. Running a script in debugging mode, using `-x` flag.

Edit the `species.sh` and introduce a typo on the `filename` varialble.

```shell
# 
for Filename in basilisk.dat minotaur.dat unicorn.dat
do
    echo $filename
    head -n 2 $filename | tail -n 1
done
```

> The `-x` prints command traces before executing the command. Notice the `echo` command doesn't have a value for `$filename`, the `filename` variable doesn't exits. Bash is case sentitive.

### 9. EXERCISE [10 mins]

Breakout session 4: [Foor Loops](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)


### 10. CLI HISTORY [10 min]

> We learned that we nagivate to previous commands executed in terminal using the up and down arrows. But there are other ways to access the command history.

a. Execute the last command

```shell
echo "hello"

!! 
```

b. Search the history with *CTRL + R*

c. Print all or parts of the history

```shell
# print all the history to the screen
history 

# print the last 5 commands
history | tail -n 5

# save the history to a file

hisotry > my-history.txt
```

> Questions?

### 11. EXERCISE 

> If time allows it.

Breakout session extra: [Challenge](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)


### 12. LESSON SUMMARY

1. The terminal or CLI is a programing inteface to interact with a computer. 
2. BASH is a programing language commonly used by the Unix terminal.
3. Unix and Windows shells are different, and commands also differ.
4. Shortcuts for directories: `.` this directory, `..` parent directory
5. Be careful when deleting files with `rm`, they will be deleted permanently.
6. `CTRL + C` will cancel/stop a program
8. Pipelines use the the `|` symbol to chain inputs and outputs between commands
7. Bash scripts and `for` loops can help to automate tasks
8. Always test your pipelines/scripts with a selected copy of your data.

