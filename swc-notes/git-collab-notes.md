# LECTURE NOTES: Quick intro to Git and Collaborative Development

**Instructor:** *Manuel G. Garcia*

**Last update:** *15-06-2022*

**Presentation:** *[Intro to version control](https://docs.google.com/presentation/d/1YcPPb0rzUXD1oYl8A8i8-XYDBwrFWzba/edit?usp=sharing&ouid=105684743155471216616&rtpof=true&sd=true)*

These notes assume the use of [Git terminal for Windows](https://gitforwindows.org/).
The context and flow of this lesson have been addapted to better fit the audience.

## PART 1: INTRO TO GIT

### Git [5 min]
> Presentation

> Version control systems start with a base version of a document and then record changes you make each step of the way.

> **Key points:**
Ask the team their experience with Git and version control.

### 1.  (OPTIONAL) SETTING UP GIT [6 min]

> **Key points:**
Use `git config` with the `--global` option to configure a user name, email address, etc.

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
* ~~Configure Default Innitial Branch.
  Change from `master` to `main`~~

    ```shell
    $ git config --global init.defaultBranch main
    ```

#### c. Check Global Settings
```shell
$ git config --global --list
```

### 2. (REFRESH) CREATING A REPOSITORY [5 min]

> **Key Points:** 
`git init` initialises a repository.
Git stores all of its repository data in a hidden `.git` directory.

#### a. Make a Directory on the Desktop
```shell
$ mkdir ~/Desktop/project
```

#### b. Initialize the Repository

```shell
$ cd ./project/
$  git init
```

#### c. Check Content and Status
```shell
$ ls -a
$ git status
```

> Explanation (slide 9): initialising (creating .git files) for every folder inside a repo is redundant and bad practice.

### 3. TRACKING CHANGES [5 min]
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

#### d. Start Tacking a File Using git add-commit
```shell
$ git add count-line.py
```

> Ignore the warning about replacing LF with CRLF. |
**Warning: LF will be replaced by CRLF in count-lines.py.
The file will have its original line endings in your working directory |**

#### e. Commit Changes 
Creates a snapshot of the changes in the repository's history three.

```shell
git commit -m "create  script count-lines.py"
```
> Explanation of **staging**. The working directory, the staging area, and the git history. `git add` is used to define which files we want to commit. `git add` specifies what changes to stage; `git commit` takes a snapshot of the changes and writes them to the repository's history. [Slides 6, 7]

### 4. GOOD COMMIT MESSAGES [5 min]

> A good commit message is short (< 50 characters), and completes the sentence: 'This will..' **message**. [Slide 8]

> `git commit -a` or `--all` "stage all changes and write them to history". `git add .` on root directoy adds all changes to staging area.

> **Questions?**

### 5. THINGS TO IGNORE [6 mins]

> **Key Points:** important  things to ignore [Slide 9]

> We'll create some fictitious data files for now.

```shell
$ mkdir data
$ touch data/a.dat data/b.dat big-data.zip
```

> **Important:** git is not good for tracking large dataset, especially binary files. This is because binary files will be fully copied to the repository history when committed, and *changes to tracked binary files will cause Git to save a copy of the files for every commit.* Therefore, increasing the size of the repository rapidly.

#### b. (Optional) Create .gitignore File
> At the root of the repository, create a `.gitignore` file, and type in it the path and name of all files and directories you don't want to track.

```shell
$ nano .gitignore
```
Type:

```shell
# data files
big-data.zip
data/
```

A good practice is to use comments to explain why files and directories are ignored. For example:

```shell
# data files:
big-data.zip
data/
```

* Add and commit .gitignore*

#### c. (Optional) Check What's Being Ignored
```shell
$ git status --ignored
```
> **Questions?**


### 8. REMOTES IN GITHUB [20 min]

> Students use their GitHub account to create an empty repository. They follow instructions to push their local copy to the remote.

> Explain remotes with GitHub **[slide 10]**

#### 0. (Optional) Conect to GitHub via SSH [Technical Break, 30 min]

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

### 9. CONFLICTS [10 min]

> Explanation of when a conflict can happen: "A conflict arises when two collaborators make changes to the same line in a file, or when a file has been deleted by one collaborator, but edited by  another." [Slide 12]

> Demo using the `count-lines.py`. A helper and the Instructor will create a conflict and present a solution.

#### a. Create conflict (Demo)

>  Repo: https://github.com/manuGil/collaborative-dev

* [Instructor]: 
    * Clone repo
    * Edit `template.md` in GitHub, commit
    * Edit `template.md` in local copy; add and commit. 
    * Pull changes from remote.

#### b. Solve conflict 
* [Instructor]: explains why the conflict occurred and how to solve it by  editing `template.md` and deciding what changes to keep. Then: adds `template.md`, and commit *withouth commit message*.
   > Explain that Git know that the conflict appeared during a merge and has prepared a commit message.
* [Instructor]: Do **push** to `origin` and shows the code in remote repo.

### 10. Branches and Forks  [8 min]

> Explain the concept of branching and forking [Slides 13, 14]

#### a. Clone workshop-check-in Repository

> Move to the Desktop and clone the workshop-check-in repo. Share the link of the repo in the chat -> `https://github.com/manuGil/collaborative-dev`

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

#### e. Demo Create branches and Pull requests [10 min]

```shell
git branch manuelg
git checkout manuelg
```

> Demo pull request on GitHub
> Demo forking on GitHub
> A note on Git in IDEs

---------
# PART 2
---------

### 13. Collaborative Development for Citien Voice 

* Description [Slide 16]
* Developemnta and Management. [Project repo](https://github.com/CUSP-Urban-Science-and-Policy/Citizen-Voice)
* Development workflow [Slide 18]
* Next Steps.
