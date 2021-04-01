# LECTURE NOTES: Version Control with Git

These lecture notes are relevant for the session on **09-April-2021**, and focuses on a beginner-level. These notes assume the using the [Git terminal for Windows](https://gitforwindows.org/).

* [Software carpentry learning material](http://swcarpentry.github.io/git-novice/)

To set up command history on two terminals do the following:

1. On main terminal:
```shell
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```shell
$ tail -f ~/.bash_history
```

> Version control systems start with a base version of a document and then record changes you make each step of the way.

## 1.  SETTING UP GIT (Lecture begins)
> Sometimes, the shortcut on the Windows menu for Git Bash won't work. In such a case: go to the installation folder (usually C:/Git) and double-click on "git-bash.exe "

> **Key points:**
Use `git config` with the `--global` option to configure a user name, email address, etc.

### Git Command Syntax

`git <verb> [options]`

### a. Setting up a username and email

```shell
$ git config --global user.name "github-username"
$ git config --global user.email "github-email@mail.com"
```

### b. Configure Line Break 

* For Windows
    ```shell
    $ git config --global core.autocrlf true
    ```
* For MacOS and Linux
    ```shell
    $ git config --gobal core.autocrlf input
    ```

### c. Check Global Settings
```shell
$ git config --list
```

### d. How to Get Help with the Commands 
> Optional: only if on schedule

```shell
$ git config -h 
```
Or (this will open HTML manual)
```shell
$ git config -help
```

## 2. CREATING A REPOSITORY 

> **Key Points:** 
`git init` initialises a repository.
Git stores all of its repository data in a hidden `.git` directory.

> **Use case:**
Two researchers/programmers are developing code to analyse the inflammation data used in the Python session.


### a. Make a Directory on the Desktop
```shell
$ mkdir ~/Desktop/patients
```

### b. Initialize Repo

```shell
$ cd ./patients/
$  git init
```

### c. Check Content and Status
```shell
$ ls -a
$ git status
```

> Explanation: initialising (creating .git files) for every folder inside a repo is redundant and bad practice.


## 3. START TRACKING CHANGES (new)
> **Key Points:** the modify-add-commit cycle.

### a. Create a Python Script to Count Lines 
> The script will count lines from the standard input

* Create file

    ```shell
    $ nano count-lines.py
    ```
* type code

    ```python
    import sys

    count = 0
    for line in sys.stdin:
        count += 1

    print(count, 'lines in standard input')
    ```
* check if the file is in the repo
    ```shell
    $ ls
    ```
### b. test the script

```shell
$ echo "this is a line" | python count-lines.py 
```

### c. Check Git Status
```shell
$ git status
```

### d. Start tacking file using git add-commit
```shell
$ git add count-lines.py
```

> Ignore the warning about replacing LF with CRLF. |
**Warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

### e. Commit Changes 
Creates a snapshot of changes in the repo's history.

```shell
git commit -m "create  script count-lines.py"
```

> `git commit -a' or "--all "stage all changes and write them to history.

> Good commit messages: short (< 50 characters).
Complete sentence: 'This will..' **message**

> Explanation of **staging**. `git add` is used to define which files we want to commit. `git add` specifies what changes to staged; `git commit` takes a snapshot of the changes and writes them to the repo's history.



## 4. MAKING OTHER CHANGES (new)

> We know that a good coding practice is using comments to describe our code. Let's add some helpful comments to our script, e.g., author, python version and a short description of what the script does.

* Add the following to the top of the script

    ```python
    """
    author: Manuel G.
    description: prints the number of lines from standard input
    """
    ```
* check status
    ```shell
    $ git status
    ```
    > Explanation of modified files and  commits]

### b. Check Differences (review changes)

```shell
$ git diff 
```

> Shows the difference between the current state and the most recently saved version (last commit)

### c. Add and Commit
```shell
git add count-lines.py
```

### d. Diff vs Diff --staged

```shell
$ git diff [do not show the difference with staged change]
$ git diff --staged [shows the difference with staged change]
```

> `git diff`: shows the difference between no-staged changes and last commit. `git diff --staged`: shows the difference between staged-changes and previous commit.

Finally,

```shell
git commit -m "add author and description".
```

## 6. GIT & DIRECTORIES (new)

### a. Create a Directory 'treatments'.
> Ask students to create a new directory, try to stage it, and check the status. 

**Solutions:**

```shell
$ mkdir treatments
```

* check the status and add the directory. No changes are added

    ```shell
    $ git status
    $ git add treatments
    $ git status
    ```
> Explanation: git doesn't track directories

### b. Create Files on the Directory and add Changes

```shell
$ touch treatments/aspirin.txt treatments/advil.txt
```

### c. Stage All Files in Directory

```shell
$ git add treatments/
$ git status
```

### d. Commit

```shell
$ git commit -m "add some treatments for patients"
```

## 8. IGNORING THINGS (new)

### a. Say you have files you don't want to tack with git

> We'll use create some fictitious data files for now.

```shell
$ mkdir data
$ touch data/a.dat data/b.dat big-data.zip
```

> **Important:** git is not good for tracking large dataset, especially binary files

### b. Create .gitignore File
> At the root of the repo, create a `.gitignore` file, and list all files and directories you don't want to tack.

```shell
$ nano .gitignore
```
Type:

```
big-data.zip
data/
```

### c. Check what's Being Ignored
```shell
$ git status --ignored
```

-------

**FRIST BREAK**

-------


## 6. EXPLORING THE HISTORY

### a. Checking the Log
```shell
$ git log
$ git log --oneline
```
> Explanation of output: unique ID and list of commit messages.

> Explanation content of Directory and where changes are stored.

> Paging the log. **Q**= quit, **spacebar**= next page, **/**=search word, **N**=navigate thru matches. `git log -N` *N*=number of commits (latest to first). `git log --oneline`, limit output to one line. `git log --graph` print a text graph of the history tree.

### b. HEAD 
> In the following parts (b-e) is more critical to **put attention** than to follow along. Put attention, follow along only if you won't lose focus.

> The **HEAD** refers to the current active branch in the git history tree. Because we haven't created any more branches. The current history tree only contains one single branch called by default *master*. In our case HEAD points to the most recent commit in the master branch. We can refer to the most recent commit using HEAD as an identifier.

### c. Let's change the author's name in our count-lines.py

```shell
$ nano count-lines.py
```
```python
# author: John J. Doe
```

### d. Check difference compared to HEAD
```shell
$ git diff HEAD treatments/aspin.txt 
```
> This is the same as not using HEAD, because the HEAD is currently pointing to the latest commit. However, we can use **HEAD** to check the difference between the current state of `count-lines.py` and previous commits.

```shell
$ git diff HEAD~1 count-lines.py 
$ git diff HEAD~3 count-lines.py
```
> `HEAD~1` compares the last commit. `HEAD~3'compares to 3 commits ago. If NO CHANGES were made between commits, the most recent change would keep displaying.

### e. Compared using the commit IDs
> "You will have to reference the SHA explicitly if you want to see the `diff` of a file that was not changed between the last commit and the one before it (HEAD~1)."

Usage:

**git diff** `<start-commit-SHA>` **HEAD** `<file>`

```shell
$ git log --oneline [copy an id to compare]
```
```shell
$ git diff commit-id count-lines.py
$ git diff commit-id HEAD count-lines.py
```

## 7. REVERTING CHANGES (new)
> **Follow along**

> BEFORE THAT: if you haven't change the author name in count-lines.py. Do that using `nano`, do not commit.

```shell
$ nano count-lines.py
```

### a. Revert to older versions using an identifier. 
>  One way to rever changes is using the commit ID. Restore the latest version. Use `chekckout`

```shell
$ git log --oneline [copy ID of HEAD]
```

```shell
$ git chekckout <id--commit> count-lines.py [will revert]
$ cat count-lines.py
```

### b. Restore version to when we added author and description
> **Aditional example. Used if on schedule**

```shell
$ git chekckout f9d7e9c count-lines.py  
```

> **Changes go to the staging area; they are not committed.** However, we always can go back to any version we have committed. To go back to the newest version, check out to HEAD.

* check out to HEAD

    ```shell
    $ git chekckout HEAD count-lines.py 
    $ cat count-lines.py [notice the file is back to the newest committed version are back]
    ```

* Commit the newest version

    ```shell
    $ git add count-lines.py 
    $ git commit -m "update author's name"
    ```


## EXERCISE 15 mins

### a. Explain exercise in plenary

Repo manipulation - (start from scratch, add files, update, recover old version - uses all that was previously shown)

### b. Helper and students go to a Breakout session

**Exercise description:** https://drive.google.com/drive/folders/1m26mHK05mSBopNrK03gg0ajho7IcReP8 


## 9. REMOTES IN GITHUB

> Students use their GitHub account to create an empty repository. They follow instructions to push their local copy to the remote.

### a. Create GitHub Repo 
> Go to Github and create an empty and public repository called 'patients-analysis'.

Repo description: *analysis of treatments for inflammation*

### b. Add Remote to Local Repo
> At your local repository (on the terminal), add the remote repo and push the content.

* connect to remote
    ```shell
    $ git remote add origin <https://url/to/your-remote-repo>
    ```

* check that remove was added
    ```shell
    $ git remote -v
    $ git branch -M main [will change the name of the main branch of the repo to make it more friendly]
    $ git push -u origin main 
    ```
> **known issue with push.** If your operating system has a password manager configured, `git push` will try to use it when it needs your username and password. In Windows, a small window might pop up, and you will need to enter your password twice (once in the terminal and once in the pop-up window. For typing the username and password only once in the terminal. Type the following before using **git push**: `unset SSH_ASKPASS`

### c. Check the repo has been completed successfully
* Go back to your repo page and refresh the browser.

* To pull changes from the remote:
    ```shell
    $ git pull origin main
    ``` 

----
**SECOND BREAK**

-------

## 10. COLLABORATING (new)

### a. Clone workshop-check-in repo
> Move to the Desktop and clone the workshop-check-in repo. Share the link of the repo in the chat -> `https://github.com/manuGil/workshop-check-in.git`

```shell
$ cd ~/Desktop
$ git clone https://github.com/manuGil/workshop-check-in.git
```
### b. Create a check-in file

> Make a copy of `check-in/template.md` in the same Directory using your first name. Mind the file extension ".md"

```shell
$ cd workshop-check-in
$ cp check-in/template.md check-in/<your-name>.md
```

### c. Edit your check-in file 
> Edit `<your-name.md>` change the content. You'll see some hints

```shell
$ nano check-in/<your-name>.md
```

### d. pull, add, commit, and push to the remote

A basic collaborative workflow using git is:

* "update your local repo with git `pull origin main`,"
* "make your changes and stage them with `git add`,"
* "commit your changes with `git commit -m', and"
* "upload the changes to GitHub with `git push origin main`"

**Example:**

```shell
$ git pull origin main
$ git add 
$ git commit -m "add check-in"
$ git push origin main
```

## 11. CONFLICTS (Demo)

> Explanation of when a conflict can happen. Demo using the `count-lines.py`. A helper and the instructor will create a conflict and present a solution.
### a. Create conflict

* [Helper]: pulls instructor repo, edits `count-lines.py` and adds his/her name as an Author. Add, commit and push changes to remote.
* [Instructor]: edits local `count-lines.py`, and adds a creation date on the comment section. Add, commit and try to push.


### b. Solve conflict 
* [Instructor]: explains why the conflict occurred and how to solve it by deciding what changes to keep.

## 14. Q&A

> Participants ask questions.
