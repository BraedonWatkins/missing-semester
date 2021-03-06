# 1. Git
- [1. Git](#1-git)
- [2. The Deep Down](#2-the-deep-down)
  - [2.1. Graphs & Directories:](#21-graphs--directories)
  - [2.2. PsuedoCode:](#22-psuedocode)
  - [2.3. SHA & Hash Functions:](#23-sha--hash-functions)
- [3. Interactive Section](#3-interactive-section)
  - [3.1. Git Branches](#31-git-branches)
    - [3.1.1. Staging vs Commit:](#311-staging-vs-commit)
    - [3.1.2. Branching Commands:](#312-branching-commands)
    - [3.1.3. Explaining `commit <SHA> (HEAD -> master)`:](#313-explaining-commit-sha-head---master)
    - [3.1.4. Note on `Fast-forward`:](#314-note-on-fast-forward)
    - [3.1.5. Note on `Merge Conflicts`:](#315-note-on-merge-conflicts)
    - [3.1.6. **Question on `Branching`:**](#316-question-on-branching)
  - [3.2. Git Remotes](#32-git-remotes)
    - [3.2.1. Remote Commands](#321-remote-commands)
- [4. Git Miscellaneous](#4-git-miscellaneous)
    - [Git Config](#git-config)
    - [Large Git Clone](#large-git-clone)
    - [Git Add Lines](#git-add-lines)
    - [Git Blame!](#git-blame)
    - [Git Stash](#git-stash)
    - [Git Bisect](#git-bisect)
    - [Git Ignore](#git-ignore)


# 2. The Deep Down  


## 2.1. Graphs & Directories:

![directory and branch](images/graphs.png)

> * foo `tree (folder)`
>   * bar.txt `blob (file)`
> * baz `tree (folder)`
>   
<br>

## 2.2. PsuedoCode:

```C
type blob = array<byte>

type tree = map <string, tree | blob>

type commit = struct {
    parents array<commit>
    String author
    String message
    tree snapshot
}

type object = blob | tree | commit
objects = map<String, object>

def store(o):
    id = SHA1(o)
    object[id] = 0

references = map <String, String>
```  
<br>


## 2.3. SHA & Hash Functions:

<p>Nothing too crazy here. Just review of hash functions</p>  
<br><br>



# 3. Interactive Section

## 3.1. Git Branches


### 3.1.1. Staging vs Commit:

<p>Nothing too crazy here. Just review of staging area and commits ("snapshots")</p>  
<br>


### 3.1.2. Branching Commands:  
<br>

|     Command     | Arguments                   |   Flags   |                   Explanation                    |
| :-------------: | :-------------------------- | :-------: | :----------------------------------------------: |
|  `git commit`   | `<blob> ` `<tree>`          | `-a` `-m` |         "Snapshot" of the current state          |
|    `git log`    |                             |   `lol`   |      Lists history of git   commits + graph      |
|    `git add`    | `<blob>`, `<tree>`          |           |  Brings files to staging area. Ready to commit.  |
| `git checkout`  | `<SHA>`, `<branch>`, `HEAD` | `-f` `-b` |          Move HEAD and preserve commits          |
|   `git diff`    | `<blob>`, `<tree>`, `<SHA>` |           |     Display which files / lines have changed     |
|  `git branch`   | `<string>`                  |   `-vv`   |         Branches off from current branch         |
|   `git merge`   | `<branch>`                  | `--abort` |       Merge `<branch>` to branch at `HEAD`       |
| `git mergetool` |                             |           | Loads configured tool to resolve merge conflicts |
<br><br>





### 3.1.3. Explaining `commit <SHA> (HEAD -> master)`:
* `master / main`: refers to commits
* `HEAD`  
<br>

### 3.1.4. Note on `Fast-forward`:
* This comes up when running `git merge <branch>` such that the current branch is a predecessor to `<branch>`
* This essentially means that the current branch will now point to where `<branch>` was pointing  
<br>

### 3.1.5. Note on `Merge Conflicts`:
* This happens when more than one branch in your merge affects the same files/lines
  * Git will try its best to auto merge but may request you to fix it 
  * If so you will have to review the code and determine how to best harmonize both pieces of code  
  <br>


### 3.1.6. **Question on `Branching`:**
* Is it best practice to keep branches relatively independent to reduce merge conflicts?  
<br><br>


## 3.2. Git Remotes


### 3.2.1. Remote Commands

|     Command      | Arguments                               |     Flags      |            Explanation             |
| :--------------: | :-------------------------------------- | :------------: | :--------------------------------: |
| `git remote add` | `<name> <url>`                          |                | Adds git remote for collaborating  |
|    `git push`    | `<remote> <localbranch>:<remotebranch>` |                | Pushes branch in remote repository |
|   `git clone`    | `<url> <localfolder>`                   |                |      Used to download a repo       |
|   `git branch`   |                                         | `set upstream` |      Checks & Creates brances      |
|   `git fetch`    |                                         |                |   Update w/ repo + Show locally    |
|   `git merge`    |                                         |                |     Move local repo to remote      |
|    `git pull`    |                                         |                |  `git fetch` + `git merge` in one  |  
<br><br>



# 4. Git Miscellaneous

### Git Config
* run `git config` or `cd ~/.gitconfig`
  * look at other git configs to find right one for you :p

### Large Git Clone
* `git clone --shalow`: gets latest snapshot not version history

### Git Add Lines
* `git add -p` (y/n): select which changes you want to keep
  * `git diff --cached`: show which changes are selected
  * `git diff`: change that will not pass
  * `git checkout`: after committing to get rid of unselected change

### Git Blame!
* `git blame <file>`: find who edited a line, at which commit, and the associated commit message
  * `git show <SHA>`: show related info to changes in commit

### Git Stash
*`git stash`: stores local changes that haven't been committed yet
  * `git stash pop`: brings stashed changes back

### Git Bisect
* `git bisect`: searches history for 

### Git Ignore
* `.gitignore`: file that is told what filetypes, patterns, directories to ignore in version control

