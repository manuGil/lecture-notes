# LECTURE NOTES: Lesson 3, Collaborative Software Development

**Instructor:** *Manuel G. Garcia*

**Last update:** *04-10-2023*

**Presentation:** *[Branching and remote operations | remote operations](https://docs.google.com/presentation/d/1p7-n04rVGNNlloMvJDAXApYkwWO1ItMIgCMLG9ScTqQ/edit#slide=id.g2512947bc00_6_14)*

<!-- **Exercises:** *[Exercises remote operations]()* -->

Lecture notes for the lesson on collaborative software development.

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

## PART 1: RECAP Operations with Remotes

### 1. MOST COMMON OPERATIONS WITH REMOTES [5 min]

> Recap figure on how local repostories and remotes are connected and how to work with remotes (Slides).

> Recap what `clone, fetch, pull` and `push` commands do.

### 2. 

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
