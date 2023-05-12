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



