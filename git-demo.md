# LECTURE NOTES: Version Control with Git

**Instructor:** *Manuel G. Garcia*

These lecture notes are relevant for the demo session on *Live Coding* as part of the Carpentry Instructor training.
During the demo session one, the trainee will be ask to live doe one of of the following episodes:

## EPISODE 1: SETTIN UP GIT

> In this episode we will learn how to set up Git after you have install Git for the first time. We will set up a **name, and email and a preferred text editor.**

> Sometimes, the shortcut on the Windows menu for Git Bash won't work. In such a case: go to the installation folder (usually `C:/Git`) and double-click on `git-bash.exe` 

> **Key points:**
Use `git config` with the `--global` option to configure a user name, email address, etc.

> Open a Git Bash terminal

### a. Git Command Syntax

`git <command> [options]`

> Explian syntax using "how to get help" as example.

* How to Get Help with the Commands: `git init -h`

#### b. Setting up a Username and Email

```bash
$ git config --global user.name "github-username"
$ git config --global user.email "github-email@mail.com"
```

#### c. Configure Line Breaks 

* For Windows
    ```shell
    $ git config --global core.autocrlf true
    ```
* For MacOS and Linux
    ```shell
    $ git config --global core.autocrlf input
    ```

### d.  Set Default Text Editor

* For Nano (Default on Git Bash)
    ```shell
    $ git config --global core.editor "nano -w"
    ```
* For Vim
    ```shell
    $ git config --global core.editor "vim"
    ```

> Link to configurations with other text editors: http://swcarpentry.github.io/git-novice/02-setup/ 

#### e. Check Global Settings
```shell
$ git config --global --list
```

## EPISODE 2: CREATING A REPOSITORY [4 min]

> **Key Points:** 
`git init` initialises a repository.
Git stores all of its repository data in a hidden `.git` directory.

> **Use case:**
One of the fortes of version control is to enable collaboration. We've been working on an escenario for planetary exploration, in which two researchers (Dracula and Wolfman) are collaboratin to send a lander to Mars, and they will use Git for version control... 


#### a. Make a Directory on the Desktop
```shell
$ mkdir ~/Desktop/planets
```

#### b. Initialize the Repository

```shell
$ cd ./planets/
$  git init
```

#### c. Change name of default branch to 'main'

```shell
$ git checkout -b main
```
#### d. Check  Status
```shell
$ git status
```
> Explanation: initialising (creating .git files) for every folder inside a repo is redundant and bad practice.

> We should be ready to track changes in our repository.

## EPISODE 3: START TRACKING CHANGES 
> **Key Points:** the modify-add-commit cycle.

> Ignore the warning about replacing LF with CRLF. |
### a. Create, Edit and save a File
> Make sure you are in `~/Desktop/planets/`

```shell
$ nano mars.txt
# Inside nano type:
Cold and dry, but everything is my favorite color
# save the changes
```

### b. Check the content of repo and  file

```shell
# check repository
$ ls
# print content of file
$ cat mars.txt
```

### c. Check Status

```shell
git status
```

### d. Add file to Staging Area

```shell
git add mars.txt

#check with git status, explain outputs
git status
```

### e. Commit Changes
Creates a snapshot of the changes in the repository's history three.

```shell
git commit -m "start notes on Mars as a base"
```
> A good commit message is short (< 50 characters), and completes the sentence: 'This will..' **message** 

**Warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

> `git commit -a` or `--all` "stage all changes and write them to history"

> Explanation of **staging**. `git add` is used to define which files we want to commit. `git add` specifies what changes to staged; `git commit` takes a snapshot of the changes and writes them to the repository's history. [Use illustration]

### f. Check Status and Log

```shell
$ git status # will not print anything

$ git log # print the repository's history (commits)

```
> Explain output of `git log`.

### g. Making other changes

- Add another line to `mars.txt`

```shell
$ nano mars.txt

# Add
The two moons may be a problem for Wolfman
```

- Add and commit changes

```shell
$ git status

# check differences compared with last commit
$ git diff # explain outputs

# try to commit directly
$ git commit -m "Add concerns about the effect of Mars' moons on Wolfman" 
```

- Add and commit the right way

```shell
$ git add mars.txt
$ git commit -m "Add concerns about the effect of Mars' moons on Wolfman" 
```  

### h. Diff vs Diff --staged

```shell
$ git diff [do not show the difference with staged change]
$ git diff --staged [shows the difference with staged change]
```

> `git diff`: shows the difference between no-staged changes and the previous commit. `git diff --staged`: shows the difference between staged-changes and the previous commit.


### i. Review the Repo's log

```shell
# full history
$ git log

# onliner
$ git log --oneline

# onliner graph
$ git log --oneline --graph

```

### j. Tracking directories

- Git doesn't track directories

```shell
$ mkdir spaceships

$ git status

$ git add spaceships

$ git status
```

- Add all files in a directory

```shell
$ touch spaceships/apollo-11 spaceships/sputnik-1

$ git status

# add all content of directory
$ git add spaceships

$ git status

$ git commit -m "Add some initial thoughts on spaceships"
