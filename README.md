# basic-git-commands
 A list of simple, useful git commands for basic project control
## Index
- [basic-git-commands](#basic-git-commands)
  - [Index](#index)
  - [**Initializing Git**](#initializing-git)
  - [**Disabling and Restoring Git**](#disabling-and-restoring-git)
  - [**Commit Related Commands**](#commit-related-commands)
    - [*View Historical Commits/Actions*](#view-historical-commitsactions)
    - [*Switching to Older Commits (Creates a New Branch)*](#switching-to-older-commits-creates-a-new-branch)
    - [*Interactive Rebase*](#interactive-rebase)
  - [**Branch Related Commands**](#branch-related-commands)
    - [*View Current Branches*](#view-current-branches)
    - [*Selecting/Switching Branches*](#selectingswitching-branches)
    - [*Creating Branches*](#creating-branches)
    - [*Viewing Branch Differences*](#viewing-branch-differences)
    - [*Merging Branches*](#merging-branches)
    - [*Renaming Branches*](#renaming-branches)
    - [*Resetting Branches*](#resetting-branches)
      - [*Resetting a Branch on Origin*](#resetting-a-branch-on-origin)
    - [*Deleting Branches*](#deleting-branches)
- [Managing Pull Requests](#managing-pull-requests)
- [**Handling Gitignore Issues**](#handling-gitignore-issues)

## **Initializing Git**
To initialize git in a project directory (will start version control)
```
git init
```
## **Disabling and Restoring Git**
To terminate git in a project directory, you can rename the .git file to something like .git_inactive, so git won't recognize the project as having vesion control.
```
mv .git .git_inactive
```
To enable git again in the project directory, you can rename the now .git_inactive folder to .git:
```
mv .git_inactive .git
```
**Make sure to Reload Window in VS Code after reinitialization by opening command palette (cmd shift p)**
## **Commit Related Commands**

### *View Historical Commits/Actions*

Simple Commit viewing:
```
git log
```
Detailed Commit Viewing:
```
git log -p
```
To view a list of all actions conducted:
```
git reflog
```
### *Switching to Older Commits (Creates a New Branch)*
The commit-hash can be retrieved using git log.
```
git checkout <commit-hash>
```
The above command will result in being in no branch. To save the commit to a new branch, execute the below command after:
```
git checkout -b <new-branch-name> 
```
The branch will contain that commit state. 
### *Interactive Rebase*
```
git rebase -i <commit-hash>
```
The above command will open an editor in the terminal (e.g. nano), with a list of all the commits *after* the selected commit SHA.

**The available commands to choose from will be listed in the open editor.**

**Note:** *If anything goes wrong during the rebase, open a new terminal window (within the project directory) and execute this command below:*

```
git rebase --abort
```
Then, close the terminal that has the interactive rebase editor open.

## **Branch Related Commands**
Branches can be used as different instances of the project. It can be useful if you want, for example, and alpha version, a main release version, and a beta version (example).
### *View Current Branches*
```
git branch
```
### *Selecting/Switching Branches*
```
git checkout <branch-name>
```
### *Creating Branches*
To create a branch and immeditely enter it to start working on it:
```
git checkout -b <new-branch-name>
```
To create a new branch, but stay on the current branch:
```
git branch <new-branch-name>
```
### *Viewing Branch Differences*
To view if branches have differing commits/changes:
```
git diff branch_name branch_name2 etc
```
Separate the branch names with a space as shown above.
### *Merging Branches*
While the branches are dissimilar, the Version Control panel will display outgoing changes. This is normal, as the branches still havn't been merged.

To Merge two branches:
```
# Switch to the branch you want to merge into
git checkout <target-branch-name>

# Merge the other branch into your current branch
git merge <source-branch-name>
```
### *Renaming Branches*
To rename the currently selected branch:
```
git branch -m <new-name>
```
To rename a specific branch:
```
git branch -m <old-name> <new-name>
```
### *Resetting Branches*
To reset branches to a specific commit state (dangerous):
```
git reset --hard <commit-hash>
```
Again, commit-hash can be retrieved with git log
#### *Resetting a Branch on Origin*
If you reset a branch locally to a specific commit, but also want the origin to be reset to that as well, you can do so like this:

1. First, reset the branch locally to a specific commit.
2. Then, you can reset the orign like so:
```
git push origin your-branch-name --force
```
**Make sure to know that doing such a thing will permanently delete all of the commits after the one you are resetting both the local and the origin branch to.**
### *Deleting Branches*
```
# For a branch that has been merged
git branch -d branch_name

# For a branch that has not been merged
git branch -D branch_name
```
# Managing Pull Requests
With git, you can retreive a pull request and create a local branch that contains the changes of those pull request.
```
git fetch origin pull/PR_NUMBER/head:BRANCH_NAME
```
In this case, replace PR_NUMBER with the number of the pull request, and replace BRANCH_NAME with the new name of the branch where that pull request will be stored.

# **Handling Gitignore Issues**
If the gitignore file does not work/is not ignoring the files in the gitignore, it most likely means that those files are already being tracked by git. So, you need to remove the cached files from the git index:
```
# Remove a single file from the Git index
git rm --cached <file>

# Remove all files in a directory from the Git index
git rm --cached -r <directory>
```
[Back to top](#basic-git-commands)