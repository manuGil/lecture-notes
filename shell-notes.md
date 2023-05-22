# LECTURE NOTES: The Unix Shell

**Instructor:** *Manuel G. Garcia*

**Last update:** *12-05-2023*

**Presentation:** *[Intro to version control]()*

These are lecture notes for the beginner-level of one of the lessons of the [Software Carpentry](https://swcarpentry.github.io/shell-novice/). These notes assume the use of [Git terminal for Windows](https://gitforwindows.org/).
The context and flow of this lesson have been addapted to better fit the audience.

## PREPARATION
The instructor sets up the command history on two terminals do the following:

1. On main terminal:
```bash
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
$ tail -f ~/.bash_history
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
### 0. INTRODUCTION [x min]

> An Quick introduction to what a BASH terminal is and what it is used for (Slides)

> Explain when and why CLIs are more useful than GUIs.

### 1. EXPLORING THE TERMINAL

a. Open Bash terminal

b. Go to the home directory

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
| `_`,  ` \|`, :white_square_button:  | text cursor | position where your typing will appear|
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

### 2. EXPLORING DIRECTORIES

#### The **p**resent **w**orking **d**irectory:

```shell
pwd
```

> Explain the how different OS represent a path to a directory differently. 

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

> Explain: alphabetically (default), by *t*ime, and in **r**everse order

b. **Clear**ing and accessing previous commands

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

> this fails because `cd` only is aware of subdirectories in current directory.

```shell
cd ../shell-lesson-data
```

> explain meaning of shortcuts: `..` and `.`

c. Changin directories using absolute paths

```shell
cd /Users/<your-user-name>/Desktop/shell-lesson-data/exercise-data
```

> Explain the use of shortcuts for navigating directories: `~/` (user-home directory), `cd` (no argument defaults to root directory), `-` location of previous directory

### 3. WORKING WITH FILES AND DIRECTORIES

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

c. Create `project/data` and `project/data` directories and its **p**arents, in *./thesis/*

```shell
mkdir -p project/data
mkdir -p project/results
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

b. Move (rename) `draft.txt` to `quotes.txt`

```shell
mv thesis/draft.txt thesis/quotes.txt
```

> Explain `mv` also works for directories

c. Copy `quotes.txt`

```shell
cp quotes.txt thesis/quotations.txt
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
rm -r Thesis
```

> Explain, be careful with `rm`. Files will be permanently deleted. To check use `rm -i`.

> Explain `cp` and `rm` accept multiple arguments.

#### Using Wildcards

> Explanation, wildcards are used to for pattern matching and they help to apply commands to multiple files and directories. Explain **\*** (one or more characters), and **?** (any one character).

a. List files in `alkanes` directory

```shell
ls *t*ane.pdb
ls *t?ne.*
ls *t??ne.pdb
ls ethane.*
```

### 4. PIPES AND FILTERS

> work on the directory `shell-lesson-data/exercise-data/alkanes`. Files with `.pdb` extension are from the *Protein Data Bank* (plain text, speficies the position of each atom in a molecule)


a. List the content of the directory

```shell
cd shell-lesson-data/exercise-data/alkanes
ls
```

b. Use the **w**rd **c**ount command to count the content of a file

```shell
wc cubane.pdb
```

> Meaning of output: number of *lines, words and characters*

c. Use `wc` and wildcard to count the countent of all files with `*.pdb` extension.

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

> What we need to do to find an aswers using the CLI? Which stemps? Ask participants to think
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
short ../../numbers.txt # aphabetically
```

```shell
short -n ../../numbers.txt # numerically
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

#### Pipelines
They combine two or more commands. The `|` symbol take the output on one command as input for another command (Slide x)

a. Sort and listing the first result

```shell
sort -n lengths.txt | head -n -1
```

b. We can combine the steps from the case above into pipelines.

```shell
# pipeline for counting and sorting
wc -l *.pdb | sort -n
```

```shell
# pipeline for counting, sourting and filtering
wc -l *.pbd | sort -n | head -n 1
```

> Questions?

### Exercise?
Nelle’s Pipeline: Checking Files: https://swcarpentry.github.io/shell-novice/04-pipefilter.html#nelles-pipeline-checking-files

### 6. SHELL SCRIPTS & LOOPS

> Scripts are list of commands (representing a program) saved to a file. They are useful, for example, when we expect to repeat the same command for different inputs.

a. Create a script to select lines 11-15 fo the `octane.pdb` file

```shell
cd alkanes
nano middle.sh
```

```shell
# content of middle.sh

head -n 15 octane.pdb | tail -n 5
```

> use **CTRL + O** to save, and **CTRL + X** to exit the editor.

b. Run the script using BASH

```shell
bash middle.sh
```

### Passing arguments to a script

> We define varialble in BASH 

a. Edit the  `middle.sh` script as follows.

```shell
head -n 15 "$1"
```

> `$1`is a place holder for a positional argument. A value must be passed when executing `middle.sh`. We use double quotes here to allow the use of spaces in the value for the argument.


> Save changes, and execute `middle.sh` again. Explain which advantages the new script has compared with the first version.

b. Define multiple arguments and and add comments

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



> What if we want to sort many files based on thier number of files. Explain use of `$@`to define a variale list of arguments

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

### Looping

> Explanation. Loops are a programming construct which allow us to repeat a command or set of commands for each item in a list. Use pseudo-code to explain `for` loops (slide)

> Use case. suppose we want to print the classificaiton of each species in the files of the `/creatures` directory. The commands that are helpful in this case are `head -n 2` and then `tial -n 1`

a. move to `/creatures` directory

```shell
cd exercise-data/creatures
```

b. Create a shell script `species.sh`, and  use a `for` loop to apply those commanad to all `.dat` files


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

> The above fails with 'cp: target original-*.data is not a directory. cp expects a directory when multiple files are passed as teh first argument.

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

> Script is executed line-by-line. Notice the `echo` command doesn't print anything, the `filename` variable doesn't exits. Bash is case sentitive.

### 7. CLI HISTORY


### 7. LESSON SUMMARY

```shell
```
> Need to decide on exercises