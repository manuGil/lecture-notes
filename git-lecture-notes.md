# LECTURE NOTES: Version Control with Git

This lecture notes are relevant for the session on **09-April-2021**, and focuses on a beginner-level. These notes assume the using the [Git terminal for Windows](https://gitforwindows.org/).

* [Software carpentry learning material](http://swcarpentry.github.io/git-novice/)

To set up command history on two terminal do the following:

1. On main terminal:
```shell
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```shell
$ tail -f ~/.bash_history
```

> Version control systems start with a base version of a document, and then record changes you make each step of the way.

## 1.  SETTING UP GIT (Lecture begins)
> Sometimes the shortcut on the Windows menu for Git Bash,  won't work. In suh a case: go to the installation folder (usually C:/Git) and double-click on ``git-bash.exe``

> **Key points:**
Use `git config` with the `--global` option to configure a user name, email address, etc.

### Git Command Syntax

`git <verb> [options]`

### a. Setting up username and email

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
```shell
$ git config -h 
```
Or (this will open HTML manual)
```shell
$ git config -help
```

## 2. CREATING A REPOSITORY

> **Key Points:** 
`git init` initializes a repository.
Git stores all of its repository data in a hidden `.git` directory.

> **Use case:**
Two researchers/progammers developing code to analyse the inflamation data used in the Python session.


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

### d. Bad practice
> Initializing (creating .git files) for every folder inside a directory.

## 3. START TRACKING CHANGES 
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
* check if file is in repo
    ```shell
    $ ls
    ```
### b. test the Script

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

> Ignore the warning about replacing LF by CRLF. |
**warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

### e. Commit Changes 
Creates a snapshot of changes in the repo's history.

```shell
git commit -m "create  script count-lines.py"
```

> Good commit messages: short (< 50 charaters).
Complete sentence: 'This will..' **message**


### f. Check Status Again & Check the Log

```shell
$ git status
$ git log 
```

> Explanation of output: unique id, and list of commit messages.

> Explanation o content of directory and where changes are stored

## 4. MAKE OTHER CHANGES

> We know that a good coding practice is using comments to discribe our code. Let's add some helpful comments to our script, e.g., author, python version and  short description of what the script does.

* Add the following to the top of the script

    ```python
    """
    author: Manuel G.
    description: prints the number of lines from standard input
    """
    ```

* checkk status
    ```shell
    $ git status
    ```
    > Explanation of modified files and  commits]

### b. Check Differences (review changes)

```shell
$ git diff 
```

> Shows the difference between current state and most recently saved version (last commit)

### c. Add and Commit
```shell
git add count-lines.py
git commit -m "add author and description"
```

## 5. STAGING

### a. What is Staging

> Explanation of **staging**. `git add` is used to define which files we want to commit. `git add` specifies what changes to staged; `git commit` takes an snapshot of the changes and writes them to the repo's history.

```shell
$ git add 
$ git commit
```

> `git commit -a` or ``--all`` stage all changes and write them to history.

### b. Difference Between git diff and git diff --staged

* Do some more changes to `count-lines.py`. E.g, add python version to script:  *python version: 3.9*

    ```shell
	$ nano count-lines.py
	$ git diff
	```

*  Stage changes and check with `diff`
    ```shell
	$ git add count-lines.py
	$ git diff 
	$ git diff --staged 
    ```

> `git diff`: shows diffeence betwen no-stagedchanges and last commit. `git diff --staged`: shows difference between staged-changes and last commit.

* commit changes
```shell
$ git commit -m "add python version to script"
```

### c. Checking the Log
```shell
$ git log
```

> Paging the log. **Q**= quit, **spacebar**= next page, **/**=search word, **N**=navigate thru matches. `git log -N` *N*=number of commits (latest to first). `git log --oneline`, limit output to one line. `git log --graph` print a text graph of the history tree.

## 6. GIT & DIRECTORIES (exercise?)

### a. Create a Directory 'treatments'
```shell
$ mkdir treatments
```

* check status and add directory. No changes are added

    ```shell
    $ git status
    $ git add spaceships
    $ git status
    ```
> git doesn't track directories

### b. Create Files on the Directory and add Changes

```shell
$ touch treatments/aspirin.txt treatments/advil.txt
```

### c. Stage All Files in directory

```shell
$ git add treatments/
$ git status
```
### d. Commit

```shell
$ git commit -m "add some treatments for patients"
```

## 7. FIRST EXERCISE (20 mintues)
Groups in break-out room.
Description:  https://docs.google.com/presentation/d/1f-bhaY0HnhymkXaYdSPVXFXNl_ZIgsfq/edit#slide=id.p2




## 6. EXPLORING THE HISTORY

### a. HEAD 
> In this part is more important to put attention than follow along. Put attention, follow along only if you won't loose the focus.

> The **HEAD** refers to the current active branch in the git history tree. Because we haven't created any more branches. The current history tree only contains one single branch called by default *master*. In our case HEAD points to the most recent commmit in the master branch.
We can refere to the most recent commit using HEAD as identifier.

### a. Let's change the author's name in our count-lines.py

```shell
$ nano count-lines.py
```
```python
# author: John J. Doe
```
### b. Check difference compared to HEAD
```shell
$ git diff HEAD treatments/aspin.txt 
```
> This is the same as not using HEAD, because the HEAD is currently pointing to the latest commit. However, we can use **HEAD** to check the difference between the current state of `count-lines.py` and previous commits.

```shell
$ git diff HEAD~1 count-lines.py 
$ git diff HEAD~3 count-lines.py
```
> `HEAD~1` compares the last commit. `HEAD~3`compares to 3 commits ago.If NO CHANGES were made betwee commits, the most recent change will keep displaying.

### d. Compared using the commit IDs
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

## 7. REVERTING CHANGES 
> **Follow along**

> BEFORE THAT: if you haven't change the author name in count-lines.py. Do that using `nano`

```shell
$ nano count-lines.py
```

### a. Restore the last change. Use `chekckout`

```shell
$ git chekckout HEAD count-lines.py

$ cat count-lines.py
```

### b. Revert to older versions using  an identifier. 

```shell
$ git log --oneline
git chekckout id--commit <file-name>
```

### c. Restore version to when we added arutho and description
> **Aditional example. Used only if there's enough time**

```shell
$ git chekckout f9d7e9c count-lines.py  
```

> **Changes go to staging area, they are not commited.** Howeve, we alway can go back to any version we have commited. To go back to the newest version. Check out to HEAD.

* chect out to HEAD

    ```shell
    $ git chekckout HEAD count-lines.py 
    $ cat count-lines.py [notice the file is back to the newest version are back]
    ```

* Commit the newest version

    ```shell
    $ git add count-lines.py 
    $ git commit -m "update author's name"
    ```
## 8. Ignoring Things [move ahead]

### a. Say you have files you don't want to tack with git

> We'll use create some fictious data files for now.

```shell
$ mkdir data
$ touch data/a.dat data/b.dat big-data.zip
```

> **Important:** git is not good for tracking large dataset, specially binary files

### b. Create .gitignore File
> At the root of the repo create a `.gitignore` fiel, and list all files and directories you don't want to tack.

```shell
$ nano .gitignore
```
Type:

```
big-data.zip
data/
```

### c. Check what's being Ignored
```shell
$ git status --ignored
```
-------

**FRIST BREAK**

-------

## 10. EXERCISE (current)- 20 mins

### a. Explain exercise in plenary

Repo manipulation - (start from scratch, add files, update, recover old version - uses all what was previously shown)

### b. Helper and students go to Breakout session

**Exercise description:** https://drive.google.com/drive/folders/1m26mHK05mSBopNrK03gg0ajho7IcReP8 


## 11. REMOTES IN GITHUB

> Students use their github account to create an empty repository, and they follow instructions to push their local copy to the remote.

### a. Create github Repo 
> Go to github and create an empty and public repository called 'patients-analysis'.

Description: analysis of treatments for inflamation

### b. Add Remote to Local Repo
> At your local repository (on the terminal), add a the remote repo and push the content.

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
> **known issue with push.** If your operating system has a password manager configured, `git push` will try to use it when it needs your username and password. In Windows, a small window migth pop up and you will need to enter your password twice (once in the terminal and once in the pop-up window. For typing the username and password only once in the terminal. Type the following before using **git push**: `unset SSH_ASKPASS`

### c. Check the repo has been completed successfully
* Go back to your repo page and refresh the browser.

* To pull chages from the remote:
    ```shell
    $ git pull origin main
    ``` 

12. Collaborating

a. Move to the Desktop and clone the workshop-check-in repo

$ cd ~/Desktop
$ git clone https://github.com/manuGil/workshop-check-in.git

b. Make a copy of `check-in/template.md` in the same directory using your first name. Mind the file extension `.md`

$ cd workshop-check-in
$ cp check-in/template.md check-in/<your-name>.md

c. Edit <your-name.md> with you personal data

$ nano check-in/<your-name>.md

d. pull, add, commit, and push to the remote

[A basic collaborative workflow would be:

update your local repo with git pull origin master,
make your changes and stage them with git add,
commit your changes with git commit -m, and
upload the changes to GitHub with git push origin master
]

$ git pull origin main
$ git add 
$ git commit -m "add chekc in"
$ git push origin main

13. CONFLICTS

a. Demo using the count-lines.py

b. Solve conflict by deciding what changes to keep.

14. QUESTIONS


























