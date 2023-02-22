# LECTURE NOTES: Version Control with Git

**Instructor:** *Manuel G. Garcia*

**Last update:** *22-02-2023*

**Presentation:** *[Intro to version control](https://docs.google.com/presentation/d/1cCQcpklA-8EXQXZJ39f5tiYhD9BFabLV/edit?usp=sharing&ouid=105684743155471216616&rtpof=true&sd=true)*

These are lecture notes for the beginner-level of one of the lessons of the [Software Carpentry](https://swcarpentry.github.io/git-novice/). These notes assume the use of [Git terminal for Windows](https://gitforwindows.org/).
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

------

## PART 1
### INTRODUCTION [10 min]
> Presentation

> Version control systems start with a base version of a document and then record changes you make each step of the way.

> Explaination of the terminal and lesson set-up.

### 1.  SETTING UP GIT (Lecture begins) [6 min]

> Sometimes, the shortcut on the Windows menu for Git Bash won't work. In such a case: go to the installation folder (usually `C:/Git`) and double-click on `git-bash.exe` 

> **Key points:**
Use `git config` with the `--global` option to configure a user-name, email address, etc.

#### Git Command Syntax

`git <command> [options]`

> Explian syntax using "how to get help" as example.

* How to Get Help with the Commands (*Type along*)

    * show help for all commands: `git --help`
    * show help for specific command: e.g., `git init -h`

#### a. Setting up a Username and Email

```bash
$ git config --global user.name "github-username"
$ git config --global user.email "github-email@mail.com"
```

#### b. Configure Line Breaks 

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

* ~~Configure Default Innitial Branch.
  Change from `master` to `main`~~

    ```shell
    $ git config --global init.defaultBranch main
    ```

### 2. CREATING A REPOSITORY [4 min]

> **Key Points:** 
`git init` initialises a repository.
Git stores all of its repository data in the hidden directory: `.git`

> **Use case:**
Two researchers/programmers are developing code to analyse the inflammation data used in the Python session.

#### a. Make a Directory on the Desktop
```shell
$ mkdir ~/Desktop/patients
```

#### b. Initialize the Repository

```shell
$ cd ./patients/
$  git init
```

#### c. Check Content and Status
```shell
$ ls -a
$ git status
```

> Explanation [**slide 9**]: initialising (creating .git files) for every folder inside a repo is redundant and bad practice.

### 3. START TRACKING CHANGES [10 min]
> **Key Points:** How git track changes and the modify-add-commit cycle.

#### a. Create a Python Script to Count Lines 
> The script will count lines from the standard input. For this Python must be accessible from the terminal. But if not, it is not essential.

* Create and modify file

    ```shell
    # Windows OS
    $ nano count-lines.py
    ```
    ```shell
    # MacOS / sublime
    $ subl count-lines.py
    ```
    ```shell
    # Linux / Vim
    $ vim count-lines.py
    ```
* Type code

    ```python
    import sys

    count = 0
    for line in sys.stdin:
        count += 1

    print(count, 'lines in standard input')
    ```
* Check that the file is in the repository
    ```shell
    $ ls
    ```
#### b. Test the Script

```shell
    # check Python is accessible from Git bash
    $ python --version
```

```shell
$ echo "this is one line" | python count-lines.py 
```

```shell
$ echo -e "this is one line, \n this is another line" | python count-lines.py 
```
> -e enable interpretation of **scape characters**, like `\n`

#### c. Check Git Status
```shell
$ git status
```

#### d. Start Tacking a File Using git add-commit
```shell
$ git add count-lines.py
```

> Ignore the warning about replacing LF with CRLF. |
**Warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

#### e. Commit Changes 
Creates a snapshot of the changes in the repository's history three.

```shell
git commit -m "create script count-lines.py"
```

> A good commit message is short (< 50 characters), and completes the sentence: 'This will..' **message**.

> Explanation of **staging**. The working directory, the staging area, and the git history. `git add` is used to define which files we want to commit. `git add` specifies what changes to stage; `git commit` takes a snapshot of the changes and writes them to the repository's history. [**Slide 10**]

> Explanation of **modify-add-commit** cycle. [**Slide 11**]

> `git commit -a` or `--all` "stage all changes and write them to history". `git add .` on root directoy adds all changes to staging area.

> **Questions?**

### 4. MAKING OTHER CHANGES [5 min]

> We know that a good coding practice is using comments to describe our code. Let's add some helpful comments to our script, e.g., author, python version and a short description of what the script does.

* Add the following to the top of the script

    ```python
    """ This module counts the number of lines in standard input
    Input: strings from the system's standard input 
    """
    ```
* check status
    ```shell
    $ git status
    ```
    > **Explanation**: Notice that modified files are automatically tracked by Git, however they are not automatically committed. This is desirable because is up to the user to decide when and what to commit to the repository's history.
    
#### b. Check Differences (review changes)

```shell
$ git diff 
```

> Shows the difference between the current state of the repository, and the most recently recorded version (last commit).  More about the [meaning of the ouput of 'git diff'](https://www.atlassian.com/git/tutorials/saving-changes/git-diff)

#### c. Add and Commit
```shell
git add count-lines.py
```

#### d. Diff vs Diff --staged

```shell
$ git diff [do not show the difference with staged change]
$ git diff --staged [shows the difference with staged change]
```

> `git diff`: shows the difference between no-staged changes and the previous commit. `git diff --staged`: shows the difference between staged-changes and the previous commit.

Finally, commit the changes:

```shell
git commit -m "add description of expected input".
```

### 5. GIT & EMPTY DIRECTORIES [4 mins]

#### a. Create a Directory 'treatments'. [1 min]
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

> **Explanation**: git doesn't track empty directories. Git tracks the content of a file (lines) and its name (including its path). 

#### b. Create Files on the Directory

Creating some dummy files in the `treatment` directory:

```shell
$ touch treatments/aspirin.txt treatments/ibuprofen.txt
```

#### c. Stage All Files in the Directory

```shell
$ git add treatments/
$ git status
```

#### d. Commit

```shell
$ git commit -m "add some treatments for patients"
```

### 6. IGNORING THINGS [6 mins]

Say you have files you don't want to tack with git. For example, data files.

> We'll create some fictitious data files for now.

```shell
$ mkdir data
$ touch data/a.dat data/b.dat big-data.zip
```

> **Important:** git is not good for tracking large dataset, especially binary files. This is because binary files will be fully copied to the repository history when committed, and *changes to tracked binary files will cause Git to save a copy of the files for every commit.* Therefore, increasing the size of the repository rapidly.

#### b. Create .gitignore File
> At the root of the repository, create a `.gitignore` file, and type in it the path and name of all files and directories you don't want to track.

```shell
$ nano .gitignore
```

A good practice is to use comments to explain why files and directories are ignored. For example:

```shell
# data files:
big-data.zip
data/
```

- Add and commit .gitignore*

#### c. Check What's Being Ignored
```shell
$ git status --ignored
```

> **Questions?**

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

> Paging the log. **Q**= quit, **spacebar**= next page, **/**=search word, **N**=navigate thru matches.  `git log --oneline`, limit output to one line. `git log --graph` print a text graph of the history tree.

#### b. HEAD 
> In the following parts (b-e) is more important to **put attention** than to follow along. Put attention, follow along only if you won't lose focus. [**Slide 12**]

> The **HEAD** is a **pointer** that refers to the *current active branch* in a git repository, which can be that last commit we made or the last commit that was checkout into the working directory. We haven't created more branches and the current history tree only contains one single branch, called by default **master** or **main**. In our case HEAD points to the most recent commit in the *master/main* branch. We can refer to the most recent commit using HEAD as an identifier.

#### c. Add more to the Documentation of count-lines.py

```shell
$ nano count-lines.py
```
```python
# Output: a string with the total number of lines
```

#### d. Check Differences Compared to HEAD [**Optional**]
```shell
$ git diff HEAD count-lines.py
```
> This is the same as not using HEAD, because the HEAD is currently pointing to the latest commit. However, we can use **HEAD** to check the difference between the current state of `count-lines.py` (in the working directory) and previous commits (on the history tree).

```shell
$ git diff HEAD~1 count-lines.py 
$ git diff HEAD~3 count-lines.py
```
> `HEAD~1` compares with **one-before** the last commit in the history. `HEAD~3` compares to **three-before** the last commit in the history. 

#### e. Comparison Using the commit IDs
> "You will have to reference the Hash explicitly if you want to see the `diff` of a file that was not changed between the last commit and the one before it (HEAD~1)."

Usage:

**git diff** `<start-commit-SHA>` **HEAD** `<file>`
> When comparing two commits IDs, **THIS compared to THAT**

```shell
$ git log --oneline # [copy an ID to compare]
```
```shell
$ git diff <commit-id> count-lines.py # [use ID for first commit]
$ git diff <commit-id> HEAD count-lines.py # [use ID for first commit]
```

> IMPORTANT: Wrap up this section by showing an illustration of the git history tree [**slide 12**]

### 7. REVERTING CHANGES [9 min]

> **Follow along**

> BEFORE THAT: if you haven't add a descripton for `Output` to count-lines.py. Do that using `nano`, and commit the changes.

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

#### a. Revert to Older Versions Using an Identifier. 
>  One way to revert changes is using the commit ID. Restore latest version in the history tree using  the `checkout` command. This commands moves a version to the working directory.

```shell
$ git log --oneline # [copy ID of "description input"]
```

```shell
$ git checkout <id--commit> count-lines.py # [will revert changes, use first commit ID]
$ cat count-lines.py
```
> The `git checkout` command bring the version of a commit-id to the working directory. To make the changes permanent, commit the current version as usual.

#### b. Restore the version without any Docstring [Optional]

> **Additional example, used only if on schedule. Ask particpants to do them by themselves.**

```shell
$ git checkout f9d7e9c count-lines.py  
```

> **Changes go to the staging area; they are not committed.** However, we always can go back to any version we have committed. To go back to the newest version, check out to HEAD.

* check out to HEAD

    ```shell
    $ git checkout HEAD count-lines.py 
    $ cat count-lines.py [notice the file is back to the newest committed version]
    ```
------

### EXERCISE: Create Repository and Track Changes [15 mins]

#### a. Explain exercise in plenary

**[Exercise description (slides):](https://docs.google.com/presentation/d/17vM2uc_wvCcw7mVMqsNud71K_QZTlcXM4rD2DygkAtk/edit?usp=sharing)**

#### b. Helpers and partcipants go to a Breakout session

> Suggestion: Share your screeen, and ask participats to try things first by themselves, then show them how to do it. Give them about 1 minute per activity `[1-6]` and then show them the answers one at the time. 

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
    6. Revert changes to the very first version of ‘research.txt’, and commit.
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
--------

## PART 3

### 8. REMOTES IN GITHUB [20 min]

> Students use their GitHub account to create an empty repository. They follow instructions to push their local copy to the remote.

> Explain what GitHub is **[slide 13, 2 min]**

#### 0. Conect to GitHub via SSH [Technical Break, 30 min]

> GitHub requires authentification via SSH to do pulls an pushes, but not for cloning. **Use illustrations** [slide 14] to explain what a SSH connection entitles.

To connect via SSH do the following:

* Create a Key-pair inside the `.ssh`  in the Home directory

    ```shell
    # move to Home directory
    $ cd ~
    # create key
    $ ssh-keygen -t ed25519 -C "your_email@example.com"
    # save to the default location and file name: ~/.ssh/id_ed25519
    ```
* Check the keys have been created

    ```shell
    $ ls ~/.ssh/
    ```

* **Windows Users**: Start the `ssh-agent` and add private key to agent. *Mac and Linux user don't have to worry about this.*

    ```shell
    # start agent
    $ eval "$(ssh-agent -s)"
    
    # add private key
    $ ssh-add ~/.ssh/id_ed25519
    ```
    > Instruct SSH to use key files in different locations: `ssh -i <path/private/keyfile>`

> Info on how to [start the ssh-agent automatically](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows)


* Copy public key to GitHub:

    ```shell
    $ clip < .ssh/id_ed25519.pub
    ```

* Go to GitHub, explain the basics of the interface and add the SSH key.

Profile > Settings > SSH and GPG keys > New SSH key > Add SSH key

* Test SSH connection

    ```shell
    $ ssh -T git@github.com
    ```
> Check everyone succeeded!

> More information on working with [SSH keys and GitHub.](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

> Check the info on [Troubleshooting SSH](https://docs.github.com/en/authentication/troubleshooting-ssh) for GitHub.

**[CALL FOR BREAK]**

#### a. Create GitHub Repo 
> Go to Github and create an empty and public repository called `patients-analysis`.

- Repo description: *analysis of treatments for inflammation*

#### b. Add Remote to Local Repo

Move back to the repo directory: `~/Desktop/
> In your local repository (on the terminal), add the remote repository and push the content.

* Connect to remote
    ```shell
    $ git remote add origin git@github.com:<user-name>/<repo-name>.git
    ```

* Check that remote was added
    ```shell
    $ git remote -v
    $ git branch -M main # [Optional if config was changed. This will change the name of the main branch of the repo to make it more friendly]
    $ git push -u origin main 
    ```

#### c. Check the Content's Repositoy is in GitHub
* Go back to your repo page and refresh the browser.

* To pull changes from the remote:
    ```shell
    $ git pull origin main
    ``` 

> **Questions?**

### d. Exploring the GitHub GUI (optional)

----
**SECOND BREAK**

> Invite several participants as collaborators to the repository [workshop-checkin](https://github.com/manuGil/workshop-checkin)

-------

## PART 4

### 9. CONFLICTS (Demo) [15 min]

> Explanation of when a conflict can happen: "A conflict arises when two collaborators make changes to the same line in a file, or when a file has been deleted by one collaborator, but edited by  another." [Slide 15]

> Demo using the `count-lines.py`. A helper and the Instructor will create a conflict and present a solution.

#### a. Create conflict

* [Instructor]: explains how to add collaborators to a repository in GitHub. He adds helper as collaborator.
* [Helper]: pulls instructor's repo; edits `count-lines.py` and modifies the print line as follows: `print(count, 'total lines in standard input)`. 
* [Helper]: Adds, commits and pushes changes to remote.
* [Instructor]: edits local `count-lines.py`; modifies the print line as follows: `print('We found', count, 'lines in standard input)` Add, commit and and try to **pull**
* [Instructor] commits changes *withouth commit message*. Explains that Git know that the conflict appeared during a merge and has prepared a commit message.  and try to **pull**.

#### b. Solve conflict 
* [Instructor]: explains why the conflict occurred and how to solve it by  editing `count-lines.py` and deciding what changes to keep. Then: adds `count-lines.py`, and commit *withouth commit message*.
   > Explain that Git know that the conflict appeared during a merge and has prepared a commit message.
* [Instructor]: Do **push** to `origin` and shows the code in remote repo.

### 10. COLLABORATING  [15 min]

> Explain the concept of social coding. [1.5 min]

#### a. Clone workshop-check-in Repository

> Move to the Desktop and clone the workshop-check-in repo. Share the link of the repo in the chat -> `https://github.com/manuGil/workshop-checkin.git`

```shell
$ cd ~/Desktop
$ git clone https://github.com/manuGil/workshop-checkin.git
```

#### b. Create a Check-in file

> Make a copy of `check-in/template.md` in the same Directory; remane the file using a unique name (e.g. three first letters of your name and the last two digits of your phone number. Mind the file extension ".md"

```shell
$ cd workshop-check-in
$ cp check-in/template.md check-in/<my-nickname-file>.md
```

#### c. Edit your Check-in file 
> Edit `<my-name-file>.md` and change the content. You'll see some hints

```shell
$ nano check-in/<my-name-file>.md
```

#### d. Pull, Add, Commit, and Push to the remote

A basic collaborative workflow using git is:

* "Update the local repo with git `pull origin main`,"
* "Make changes and stage them with `git add`,"
* "Commit changes with `git commit -m`, and"
* "Upload the changes to GitHub with `git push origin main`"

**Example:**

```shell
$ git pull origin main
$ git add .
$ git commit -m "check manuel in"
$ git push origin main #[This works only if participants are added to the repository as collaborators]
```
> Ask a participant to push their changes to remote, and show the changes in the GitHuh GUI.

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
- Don't include large datasets (in binary) in your repositories. Set a `.gitignore` file
- Remotes store copies of the git repositories (e.g., GitHub, GitLab)
- Collaborative workflow using branches: **pull, add, commit, push, pull request**
- Be aware of *conflicts*

### 12. [Optinal] Licencing and Citation [5 min]

> Explaing the importance of licencing and citation for Open Science. Share template for compliance with TU Deflt software policy: https://github.com/manuGil/fair-code 

> A note on Git in IDEs

### 13. Q&A

> Participants ask questions.
