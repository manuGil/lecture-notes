# LECTURE NOTES: Lesson 2, Remotes

**Instructor:** *Manuel G. Garcia*

**Last update:** *12-06-2023*

**Presentation:** *[Branching and remote operations | remote operations](https://docs.google.com/presentation/d/1p7-n04rVGNNlloMvJDAXApYkwWO1ItMIgCMLG9ScTqQ/edit#slide=id.g2512947bc00_6_14)*

<!-- **Exercises:** *[Exercises remote operations]()* -->

Lecture notes for the lesson on remote operations with Git. 

## PREPARATION
The instructor sets up the command history on two terminals do the following:

1. On main terminal:
```bash
 export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
 tail -f ~/.bash_history | nl -w 3
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

## PART 1: Operations with Remotes

### 1. WHAT ARE REMOTE REPOSITORIES? [7 min]

> Definition of remotes. Explain the benefits of storing remote copies of source code  (Slides)

> Explain figure on how local repostories and remotes are connected and how to work with remotes (Slides)

> Explain what `fetch, pull` and `push` commands do

### 2. CREATING REMOTE REPOSITORIES [25 min]

We conntinue working with the repository of the previous lesson in `~/Desktop/2306-git/L12/git`

#### Creating a **bare** repository to serve as remote

A **bare repository** is a special type of Git repository that can be used as a remote. Non-bare repositories are 'normal' repository, like the ones who have created so far. The distinction between *bare* and *non-bare* repositories is  beyond the scope of this lesson, and something you won't have to concerned with (platforms line GitHub, and Gitlab handle that for you), unless you aim to manage remotes in your own platform.

> First we will rename the `git\` repository for convenience

a. On the terminal. Move the parent directory of the `git` repository.

```shell
cd ~/Desktop/2306-git/L12/
```

b. Rename the `git\` directory to `local`


> Notice that change the name of the root directory of a Git repository won't affect the tracking of changes or the history

```shell
mv ./git/ local
```

c. Create a new bare repository called **remote.git** and initialize it as a *bare* repository. 

> It is a convention to name bared repositories with the extension `.git`

```shell
git init --bare my_remote.git
```

d. Go into `remote.git/` and verify that indeed it is a bare Git repository

```shell
cd ./remote.git/ # notice the name of the branch is (BARE:main)
```

#### Setting a remote on an existing repository

> Now, we will see how to set a remote on an existing repository.

a. Got to the `local` repository and try to list the remotes

```shell
cd ~/Desktop/2306-git/L12/local
git remote
```

> You will see that nothing is listed. This means the repository has no remotes associated with it

b. Add a remote to the `local` repository. We will call the remote **origin**, and set the path to `my_remote.git`

```shell
git remote add origin ~/Desktop/2306-git/L12/remote.git # remote-name | URL-PATH
```
> To change the URL-PATH to the remote, use `git remote set-url <remote-name> <remote_url>`

c. Try to list the remotes again

```shell
git remote # or
git remote -v # v stands for verbose, you will see the URL or PATH
```
> A repository can have more than one remotes. The command above will list all of them.

> Also notice that there's remote for `fetch` and one for `push`. These are two basic operations with remotes.

### Pushing changes to a remote

a. Push changes from the *local* to the *remote*

```shell
# this acts on the current branch
git push -u origin main # remote-name | branch-name on the remote
```

> **-u** short hand for set-upstream. An upstream branch refers to the remote branch that your local branch is tracking or associated with. 

> You can repeat the push for every local branch you want to track in the remote. You have to be in the branch that you intend to push.

> **DRILL:** Add branches **B1** and **B1** to tracked to the remote.

b. Once the push was successful, you can inspect the remote with **git remote show**

```shell
git remote show origin
```

c. Go to the directory of the remote repository and check that the history have been transfered.

```shell
cd ../my_remote.git
git log --oneline
```
> You should see the same history of your *local* repository.

d. Go back to the `local` repository, while in the **main** branch add a new line to the `lines.txt` file, make a commit,  and push changes to the remote.


```shell
cd ../local
# add line to line.txt
echo "first line from local repo" >> lines.txt
# commit
git add lines.txt
git commit -m "add new line to local repo"
# push to the remote
git push origin # git push will have the same effect
```
e. Confirm that the change have been transfer to the log of the remote.

### 3. CLONING REMOTE REPOSITORIES [15 min]

Cloning a repository means creating a local copy of a remote repository. When you clone a repository, you download the entire history, files, and default branch of the remote repository onto your local machine. This allows you to work with the code and version history locally, make changes, and contribute to the remote.

a. On `~/Desktop/2306-git/L12/` create a direcory called **cloned**

```shell
mkdir cloned
```
b. Inside `cloned`, clone the `my-remote.git` remote repotory.

```shell
git clone ~/Desktop/2306-git/L12/my_remote.git # use full path
```
> a directory called `my_remote.git` will be created, which is a copy of the remote repository, containing all the files and history in the remote. The cloned repository is not BARE.

c. Inspect the cloned of `my_remote.git`

```shell
cd my_remote/
# list content
ls
# check the history
git log --oneline
# check the remotes
git remote -v 
```
> Notice that when you cloned a remote repository, the **origin** is set automatically. 

```shell
# check the branches
git branch
```
> notice only the main branch appears. By default the **cloned** repository only has a *main/master* branch (similar to when you initialize a repository), all other branches in the remote are hidden.

```shell
# check all remote branches
git branch -a
```

> Notice that the remote branches have path that is different than before. For example `remotes/origin/B1`. Origin is the default name that Git gives to the server/source you cloned from.


> **DRILL:** Add another line to the `lines.txt` file in the `cloned/remote/` repository `main` branch, commit the change, and **push** it to the remote. 

> "The command `git push` works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their work first and incorporate it into yours before you’ll be allowed to push" -Git Book

### 4. COMPARIGN AND SYNCING CHANGES BETWEEN REMOTE AND LOCAL REPOSITORIES [ 10 mins]

a. Go to the `/local` repository. Inspect the remote repository **origin**

```shell
git remote show origin
```

> Notice that after we pushed change from the *cloned* repository, the main branch of the *local* repo is out of date.

b. Knowing that our *local* main branch is not up to date, we can compare the versions in the remote and local repositories, using `git diff`

```shell
git diff origin/main
```

> Explain. Despite we know that the remote has changes that the local has not, nothing is shown. This is because we need to retrieve updates (commits, branches, tags) from the remote to out local repository before we can compare chages.

> For comparing specific files you can use `git diff <remote>/<branch>:<path-to-file> <path/to/local-file>`

c. Fetch update from the remote

```shell
git fetch origin
```

d. Try to compare the remote and local repositories, again.


```shell
git diff origin/main
```

> You should see that the local repository is missing the line(s) you added to the cloned repository. 

e. To retrieve updates from the remote and merge them, we can use the `git pull` command. Let's merge the in the remote to our local repository. Git

```shell
git pull origin
```

```shell
# check the lines.txt file was updated with
cat lines.txt 
```

> `git pull` combined the `git fetch` and `git merge` commands.


-----------------
## BREAK 
-----------------
## PART 2


### 4. EXERCISE [20 mins]

Breakout session 1: [Working with remote repositories](https://docs.google.com/presentation/d/1p7-n04rVGNNlloMvJDAXApYkwWO1ItMIgCMLG9ScTqQ/edit#slide=id.g2513f0e7587_19_19)

> More on remotes: https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes 

> Questions?

### 12. LESSON SUMMARY [10 min]

1. A remote is a version of a Git repository hosted in the Internet/Network.
2. Remote repositories enable distributed version control and collaboration.
3. Local repositories can be associated to one or more remotes.
4. `git clone` clones are remote repository to a local computer
5. `git push` push changed from a local to a remote repository.
6. `git pull` involves two operations `git fetch` and `git merge`.
7. Remote and local repositories do not sync automatically. 
