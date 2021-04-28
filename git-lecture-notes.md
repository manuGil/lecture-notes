# LECTURE NOTES: Version Control with Git

These lecture notes are relevant for the session on **09-April-2021**, and focuses on a beginner-level. These notes assume the using the [Git terminal for Windows](https://gitforwindows.org/).

* [Software carpentry learning material](http://swcarpentry.github.io/git-novice/)

To set up command history on two terminals do the following:

1. On main terminal:
```bash
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
$ tail -f ~/.bash_history
```

### Windows Terminal (Preview) [Keboard shortcuts]

| Action             | Shortcut                |
|--------------------|--------------------------|
|Split pane horizontally | Alt + Shift + `-`   | 
|Split pane vertically   | Alt + Shift + `+`   |
|Close a pane            | Ctrl+Shift + `w`     |
|Move pane focus         | Alt + `Arrow keys`   |
|Resize the focused pane | Alt+Shift + `Arrow keys` |

------

## PART 1
### INTRO [10 min]

> Version control systems start with a base version of a document and then record changes you make each step of the way.

### 1.  SETTING UP GIT (Lecture begins) [6 min]
> Sometimes, the shortcut on the Windows menu for Git Bash won't work. In such a case: go to the installation folder (usually `C:/Git`) and double-click on `git-bash.exe` 

> **Key points:**
Use `git config` with the `--global` option to configure a user name, email address, etc.

#### Git Command Syntax

`git <command> [options]`

> explian syntax using "how to get help" as example.

* How to Get Help with the Commands 

    * show help for all commands: `git --help`
    * show help for specific command: e.g., `git init -h`

#### a. Setting up a username and email

```bash
$ git config --global user.name "github-username"
$ git config --global user.email "github-email@mail.com"
```

#### b. Configure Line Break 

> Use Notepad++ to demo the line breaks

* For Windows
    ```shell
    $ git config --global core.autocrlf true
    ```
* For MacOS and Linux
    ```shell
    $ git config --global core.autocrlf input
    ```

#### c. Check Global Settings
```shell
$ git config --global --list
```


### 2. CREATING A REPOSITORY [4 min]

> **Key Points:** 
`git init` initialises a repository.
Git stores all of its repository data in a hidden `.git` directory.

> **Use case:**
Two researchers/programmers are developing code to analyse the inflammation data used in the Python session.


#### a. Make a Directory on the Desktop
```shell
$ mkdir ~/Desktop/patients
```

#### b. Initialize Repo

```shell
$ cd ./patients/
$  git init
```

#### c. Check Content and Status
```shell
$ ls -a
$ git status
```

> Explanation: initialising (creating .git files) for every folder inside a repo is redundant and bad practice.


### 3. START TRACKING CHANGES (new) [10 min]
> **Key Points:** the modify-add-commit cycle.

#### a. Create a Python Script to Count Lines 
> The script will count lines from the standard input

* Create and modify file

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
#### b. test the script

```shell
$ echo "this is a line" | python count-lines.py 
```

#### c. Check Git Status
```shell
$ git status
```

#### d. Start tacking file using git add-commit
```shell
$ git add count-lines.py
```

> Ignore the warning about replacing LF with CRLF. |
**Warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

#### e. Commit Changes 
Creates a snapshot of changes in the repo's history.

```shell
git commit -m "create  script count-lines.py"
```

> `git commit -a' or "--all "stage all changes and write them to history.

> Good commit messages: short (< 50 characters).
Complete sentence: 'This will..' **message** [use slide] 

> Explanation of **staging**. `git add` is used to define which files we want to commit. `git add` specifies what changes to staged; `git commit` takes a snapshot of the changes and writes them to the repo's history. Use illustration.

> **Questions?**

### 4. MAKING OTHER CHANGES (new) [5 min]

> We know that a good coding practice is using comments to describe our code. Let's add some helpful comments to our script, e.g., author, python version and a short description of what the script does.

* Add the following to the top of the script

    ```python
    """ This module counts the number of lines in standard input
    Input: any string from system standard input 
    """
    ```
* check status
    ```shell
    $ git status
    ```
    > Explanation of modified files and  commits

#### b. Check Differences (review changes)

```shell
$ git diff 
```

> Shows the difference between the current state and the most recently saved version (last commit)

#### c. Add and Commit
```shell
git add count-lines.py
```

#### d. Diff vs Diff --staged

```shell
$ git diff [do not show the difference with staged change]
$ git diff --staged [shows the difference with staged change]
```

> `git diff`: shows the difference between no-staged changes and last commit. `git diff --staged`: shows the difference between staged-changes and previous commit.

Finally,

```shell
git commit -m "add description of expected input".
```

### 5. GIT & DIRECTORIES (new) [4 mins]

#### a. Create a Directory 'treatments'.
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

#### b. Create Files on the Directory and add Changes

```shell
$ touch treatments/aspirin.txt treatments/advil.txt
```

#### c. Stage All Files in Directory

```shell
$ git add treatments/
$ git status
```

#### d. Commit

```shell
$ git commit -m "add some treatments for patients"
```

### 6. IGNORING THINGS (new) [6 mins]

#### a. Say you have files you don't want to tack with git

> We'll use create some fictitious data files for now.

```shell
$ mkdir data
$ touch data/a.dat data/b.dat big-data.zip
```

> **Important:** git is not good for tracking large dataset, especially binary files

#### b. Create .gitignore File
> At the root of the repo, create a `.gitignore` file, and list all files and directories you don't want to tack.

```shell
$ nano .gitignore
```
Type:

```
big-data.zip
data/
```

* Add and commit .gitignore*


#### c. Check what's Being Ignored
```shell
$ git status --ignored
```

-------

**FIRST BREAK** 

-------

## PART 2

### 7. EXPLORING THE HISTORY [16 min]

#### a. Checking the Log
```shell
$ git log
$ git log --graph [optional]
$ git log --oneline
```


> Explanation of output: unique ID and list of commit messages.

> Explanation content of Directory and where changes are stored.

> Paging the log. **Q**= quit, **spacebar**= next page, **/**=search word, **N**=navigate thru matches. `git log -N` *N*=number of commits (latest to first). `git log --oneline`, limit output to one line. `git log --graph` print a text graph of the history tree.

#### b. HEAD 
> In the following parts (b-e) is more critical to **put attention** than to follow along. Put attention, follow along only if you won't lose focus.

> The **HEAD** refers to the *current active branch* in the git history tree. Because we haven't created any more branches. The current history tree only contains one single branch, called by default **master** or **main**. In our case HEAD points to the most recent commit in the *master/main* branch. We can refer to the most recent commit using HEAD as an identifier.

#### c. Let's add some documentation about the ouput of count-lines.py

```shell
$ nano count-lines.py
```
```python
# Output: a string with the total number of lines
```

#### d. Check difference compared to HEAD
```shell
$ git diff HEAD count-lines.py
```
> This is the same as not using HEAD, because the HEAD is currently pointing to the latest commit. However, we can use **HEAD** to check the difference between the current state of `count-lines.py` and previous commits.

```shell
$ git diff HEAD~1 count-lines.py 
$ git diff HEAD~3 count-lines.py
```
> `HEAD~1` compares the last commit. `HEAD~3'compares to 3 commits ago. 

#### e. Compared using the commit IDs
> "You will have to reference the SHA explicitly if you want to see the `diff` of a file that was not changed between the last commit and the one before it (HEAD~1)."

Usage:

**git diff** `<start-commit-SHA>` **HEAD** `<file>`

```shell
$ git log --oneline # [copy an ID to compare]
```
```shell
$ git diff commit-id count-lines.py # [use ID for first commit]
$ git diff commit-id HEAD count-lines.py # [use ID for first commit]
```
> wrap up this section by an illustration of the git history tree

### 7. REVERTING CHANGES (new) [9 min]
> **Follow along**

> BEFORE THAT: if you haven't add a descripton for `Output` to count-lines.py. Do that using `nano`, and commit!

```shell
$ nano count-lines.py
```
```python
# Output: a string with the total number of lines
```

```shell
$ git add count-lines.py
$ git commit -m "add description of output"
```

#### a. Revert to older versions using an identifier. 
>  One way to rever changes is using the commit ID. Restore the latest version. Use `checkout`

```shell
$ git log --oneline # [copy ID of "description input"]
```

```shell
$ git checkout <id--commit> count-lines.py # [will revert changes, use firts commit ID]
$ cat count-lines.py
```

#### b. Restore version to without any docstring [Optional]
> **Aditional example. Ask particpants to do it. Used if on schedule**

```shell
$ git checkout f9d7e9c count-lines.py  
```

> **Changes go to the staging area; they are not committed.** However, we always can go back to any version we have committed. To go back to the newest version, check out to HEAD.

* check out to HEAD

    ```shell
    $ git checkout HEAD count-lines.py 
    $ cat count-lines.py [notice the file is back to the newest committed version are back]
    ```

* Add and Commit the newest version

    ```shell
    $ git add count-lines.py 
    $ git commit -m "update author's name"
    ```
------

### EXERCISE [15 mins]

#### a. Explain exercise in plenary

**Exercise description (slides):** https://docs.google.com/presentation/d/17vM2uc_wvCcw7mVMqsNud71K_QZTlcXM4rD2DygkAtk/edit?usp=sharing

#### b. Helpers and partcipants go to a Breakout session

> Suggestion: Share your screeen, and ask participats to try things firts by themselves, then show them how to do it. Give them about 1 minute per activity `[1-6]` and then show them the answers one at the time. 

#### c. Answers

* **Create new repository, use the modify-add-commit cycle, and recover older versions.**

    1. Create and initialize a repository called ‘my-repo’. 

        ```shell
        $ mkdr my-repo
        $ cd my-repo/
        $ git init
        ```
    2. Create a files `research.txt` with the sentence: **Science is awesome**

        ```shell
        $ nano research.txt
        ```
        Inside the file type the following and save changes:
        ```shell
        Science is awesome
        ```
    3. Add and commit the changes. Remember to use a meaning message.
        
        ```shell
        $ git add research.txt
        $ git commit -m "add awesome science"
        ```
    4. Change sentence in ‘research.txt’ to: **Science is messy**
        ```shell
        $ nano research.txt
        ```
        Change text to this and save changes:
        ```shell
        Science is messy
        ```
    5. Add and commit.
        ```shell
        $ git add research.txt
        $ git commit -m "change to messy science"
        ```
    6. Revert changes to very first version of ‘research.txt’, and commit.
        ```shell
        $ git log --oneline # find and copy ID of the firts commit
        $ git checkout <commit-ID> research.txt # revert changes 
        $ cat reseach.txt # check version has been recovered
        $ git commit -m "recover awesome science" # commit recovered version
        ```

* **Check your history log – you should have 3 commits**

    ```shell
    $ git log # print full log
    $ git log --graph # print log as text-graph
    $ git log --oneline # print short version of log
    ```
-----

## PART 3

### 8. REMOTES IN GITHUB [10 min]

> Students use their GitHub account to create an empty repository. They follow instructions to push their local copy to the remote.

> Explain what GitHub is **[slides, 2 min]**

#### a. Create GitHub Repo 
> Go to Github and create an empty and public repository called `patients-analysis`.

Repo description: *analysis of treatments for inflammation*

#### b. Add Remote to Local Repo
> At your local repository (on the terminal), add the remote repo and push the content.

* connect to remote
    ```shell
    $ git remote add origin <https://url/to/your-remote-repo>
    ```

* check that remote was added
    ```shell
    $ git remote -v
    $ git branch -M main [will change the name of the main branch of the repo to make it more friendly]
    $ git push -u origin main 
    ```
> **known issue with push.** If your operating system has a password manager configured, `git push` will try to use it, when it needs your username and password. In **Windows**: a small window might pop up, and you will need to enter your password twice (once in the terminal and once in the pop-up window. For typing the username and password only once in the terminal. Type the following before using **git push**: `unset SSH_ASKPASS`

#### c. Check the repo has been completed successfully
* Go back to your repo page and refresh the browser.

* To pull changes from the remote:
    ```shell
    $ git pull origin main
    ``` 

> Questions?

### d. Exploring the GitHub GUI (optional)

----
**SECOND BREAK**

-------

## PART 4

### 9. CONFLICTS (Demo) [15 min]

> Explanation of when a conflict can happen: "A conflict arises when two separate branches have made edits to the same line in a file, or when a file has been deleted in one branch but edited in the other."

> Demo using the `count-lines.py`. A helper and the Instructor will create a conflict and present a solution.

#### a. Create conflict

* [Helper]: pulls instructor repo; edits `count-lines.py` and modifies the print line as follows: `print(count, 'total lines in standard input)`. 
* [Helper]: Add, commit and push changes to remote.
* [Instructor]: edits local `count-lines.py`; modifies the print line as follows: `print('We found', count, 'lines in standard input)` Add, commit and try to **pull**.

#### b. Solve conflict 
* [Instructor]: explains why the conflict occurred and how to solve it by deciding what changes to keep. Then: add, commit, **push**.


### 10. COLLABORATING (new) [15 min]

> Explain the concept of social coding. [1.5 min]

#### a. Clone workshop-check-in repo
> Move to the Desktop and clone the workshop-check-in repo. Share the link of the repo in the chat -> `https://github.com/manuGil/workshop-check-in.git`

```shell
$ cd ~/Desktop
$ git clone https://github.com/manuGil/workshop-check-in.git
```

#### b. Create a check-in file

> Make a copy of `check-in/template.md` in the same Directory using your first name. Mind the file extension ".md"

```shell
$ cd workshop-check-in
$ cp check-in/template.md check-in/<your-name>.md
```

#### c. Edit your check-in file 
> Edit `<your-name.md>` change the content. You'll see some hints

```shell
$ nano check-in/<your-name>.md
```

#### d. pull, add, commit, and push to the remote

A basic collaborative workflow using git is:

* "update your local repo with git `pull origin main`,"
* "make your changes and stage them with `git add`,"
* "commit your changes with `git commit -m`, and"
* "upload the changes to GitHub with `git push origin main`"

**Example:**

```shell
$ git pull origin main
$ git add .
$ git commit -m "check manuel in"
$ git push origin main #[This will one work  if participants are adde to the repo as collaborators]
```
> Ask a participant to push their changes to remote

#### e. [Optional] Demo Create branches and Pull requests 

```shell
git branch manuelg
git checkout manuelg
```
> Demo pull request on GitHub

### 11. LESSON SUMMARY [2 min]
- Repository initialization `git init`
- Git records changes via commits to the history three
- Remember the **modify-add-commit** cycle
- Don't include large datasets in your repositories. Set a `.gitignore` file
- Remotes store copies of the git repositories (e.g., GitHub, GitLab)
- Collaborative workflow: **pull, add, commit, push**
- Be aware of *conflicts*

### 12. [Optinal] Licencing and Citation [5 min]

> Explaing the importance of licencing and citation for Open Science. 


### 13. Q&A

> Participants ask questions.
