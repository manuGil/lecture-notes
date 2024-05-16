# LECTURE NOTES: Lesson 3, Collaborative Software Development

**Instructor:** *Manuel G. Garcia*

**Last update:** *13-06-2023*

**Presentation:** *[Collaborative development for research software]()*

**Exercises:** *[Exercises collaborative development]()*

Lecture notes for the episode on collaborative development for research software. 

## PREPARATION
The instructor sets up the command history on two terminals do the following:

1. On main terminal:
```bash
$ export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
$ tail -f ~/.bash_history | nl -w 3
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

## PART 1: Collaborative development for research software

### 1. WHEN TO AIM FOR A COLLABORATIVE APPROACH?


> An Quick introduction to collaborative development. Definitions  (Slides)

> Explain the difference between private and close collaboration


### 2. MANAGEMENT STRATEGIES [10 min]


> Explain why manamgement is importatn for developmen software, teh key factors to consider and remcommend a management strategy based on experience.

### 3. ROLES AND RESPONSIBILITIES


> Explain why manamgement is importatn for developmen software, the key factors to consider and remcommend a management strategy based on experience.

> Describe the responsibilities for each role and why they are important for a research-software development project.

### 4. EXERCISE [6 min]

Breakout session 1: [Make Teams](#)

### 5. COLLABORATIVE PLATFORMS

#### 0. Conect to GitHub via SSH [ 10 min]

> Ask participants if this is necessary.

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

### 6. INVITING COLLABORATORS

> Participants are invited as collaborators to the check-in repository. Participants have permission to merge pull requets.

a. Demo on how to invite collaborators using the check-in repository.




### EXERCISE [6 min]

Breakout session 1: [Check in workshop](#)

b. Show how to push changes to the remote *workshop-checkin*

> Show the changes in GitHub.



### 7. FORKS AND PULL REQUESTS.

a. Use the *workshop-checking* repository to show how we can avoid the issue with pulling and pushing on the same branch. 

> Change from type-along to asking participants to do so. 

b. Create a feature branch for each participant, and change to it.

c. Make change to the participants copy of `template.md`. Commit changes and push changes upstream.

d. Show branches in web GUI.

e. Show participants how to create pull request. They create a pull request for their branches to main. 

f. Participants accept and  merge their own pull requests.

g. Explain what forks are and how to create them. They create a work of `workshop-checkin` to their accounts.

> Explain that forks have the advantage of not requiring that potential collaborators are invited to a repo. 

### EXERCISE [10 min]

Breakout session 3: [Forks on Workhop-checkin](#)

> Show the changes in GitHub.

### 8. Documenting issues

> Explain what issue are, and some best practices (slide)

a. Show participants how to open an issue using the forked repo from the previous exercise.

### EXERCISE [4 min]

a. ask participants to create 2 or 3 ficticious issues on the fork of the previous exercise.

### 9. COLLABORATIVE WORFLOWS. 

[CONTINUE HERE]


-----------------
## BREAK [10 min]
-----------------
## PART 2

### 4. EXERCISE [10 mins]

Breakout session 1: [Files & Directories](https://docs.google.com/presentation/d/13Bnf8ADO5N3L0e0i6W_mTCiuIbE1hrO3HR7dRTx0BS4/edit?usp=sharing)



### 12. LESSON SUMMARY

1. The terminal or CLI is a programing inteface to interact with a computer. 
2. BASH is a programing language commonly used by the Unix terminal.
3. Unix and Windows shells are different, and commands also differ.
4. Shortcuts for directories `.` this directory, `..` parent directory
5. Be careful when deleting files with `rm`, they will be deleted permanently.
6. `CTRL + C` will cancel/stop a program
8. Pipeline use the the `|` symbol to chain inputs and outputs between commands
7. Bash scripts and `for` loops can help to automate tasks
8. Always test your pipelines/scripts with a selected copy of your data.

