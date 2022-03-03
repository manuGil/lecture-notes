# LECTURE NOTES: Version Control with Git

**Instructor:** *Manuel G. Garcia*

**Last update:** *20-02-2022*

These lecture notes for the beginner-level of one of the lessons of the [Software Carpentry](https://swcarpentry.github.io/git-novice/). These notes assume the use of [Git terminal for Windows](https://gitforwindows.org/).
The context and flow of this lesson have been addapted to better fit the audience.

## PART 3

### 8. REMOTES IN GITHUB [20 min]

> Students use their GitHub account to create an empty repository. They follow instructions to push their local copy to the remote.

> Explain what GitHub is **[slides, 2 min]**

#### 0. Conect to GitHub via SSH [Technical Break, 10 min]

> Recently, GitHub requires authentification via SSH to do pulls an pushes, but not for cloning. **Use illustrations** to explain what a SSH connection entitles.

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

* Start the `ssh-agent` and add private key to agent:

    ```shell
    # start agent
    $ eval "$(ssh-agent -s)"
    
    # add private key
    $ ssh-add ~/.ssh/id_ed25519
    ```
    > Instruct SSH to use key files in different locations: `ssh -i <path/private/keyfile>`

> Info on how to (start the ssh-agent automatically)[https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows]
Mac and Linux user don't have to worry about this.

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

> More information on working with (SSH keys and GitHub.)[https://docs.github.com/en/authentication/connecting-to-github-with-ssh]

> Check the info on (Troubleshooting SSH[https://docs.github.com/en/authentication/troubleshooting-ssh]) for GitHub.

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
    $ git branch -M main # [will change the name of the main branch of the repo to make it more friendly]
    $ git push -u origin main 
    ```

#### c. Check the Content Repositoy is in GitHub
* Go back to your repo page and refresh the browser.

* To pull changes from the remote:
    ```shell
    $ git pull origin main
    ``` 

> Questions?

### d. Exploring the GitHub GUI (optional)

----
**SECOND BREAK**

> Invite several participants as collaborators to the repository `workshop-check-in`

-------

## PART 4

### 9. CONFLICTS (Demo) [15 min]

> Explanation of when a conflict can happen: "A conflict arises when two collaborators make changes to the same line in a file, or when a file has been deleted by one collaborator, but edited by  another."

> Demo using the `count-lines.py`. A helper and the Instructor will create a conflict and present a solution.

#### a. Create conflict

* [Instructor]: explains how to add collaborators to a repository in GitHub. He adds helper as collaborator.
* [Helper]: pulls instructor's repo; edits `count-lines.py` and modifies the print line as follows: `print(count, 'total lines in standard input)`. 
* [Helper]: Adds, commits and pushes changes to remote.
* [Instructor]: edits local `count-lines.py`; modifies the print line as follows: `print('We found', count, 'lines in standard input)` Add, commit and try to **pull**.

#### b. Solve conflict 
* [Instructor]: explains why the conflict occurred and how to solve it by  editing `count-lines.py` and deciding what changes to keep. Then: add, commit,and  **push**.

### 10. COLLABORATING  [15 min]

> Explain the concept of social coding. [1.5 min]

#### a. Clone workshop-check-in Repository

> Move to the Desktop and clone the workshop-check-in repo. Share the link of the repo in the chat -> `https://github.com/manuGil/workshop-checkin.git`

```shell
$ cd ~/Desktop
$ git clone https://github.com/manuGil/workshop-check-in.git
```

#### b. Create a Check-in file

> Make a copy of `check-in/template.md` in the same Directory; remane the file using a unique name (e.g. three first laters of your name and the last two digits of your phone number. Mind the file extension ".md"

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
> Ask a participant to push their changes to remote, and show the changes int the GitHuh GUI.

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
- Collaborative workflow using branches: **pull, add, commit, push, pull request**
- Be aware of *conflicts*

### 12. [Optinal] Licencing and Citation [5 min]

> Explaing the importance of licencing and citation for Open Science. Share template for compliance with TU Deflt software policy: https://github.com/manuGil/fair-code 


### 13. Q&A

> Participants ask questions.
