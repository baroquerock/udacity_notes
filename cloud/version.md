# Version control

## Terminology

**Version Control System (VCS)** / **Source Code Manager (SCM)** - a tool that manages different versions of source code

**Commit** - a snapshot of the state of a project (like a save point in a game)

**Repository** - a directory which contains your project work (made up of commits)

**Checkout** - when content in the repository has been copied to the Working Directory

**Staging Area** / **Staging Index** / **Index** - a file in the Git directory that stores information about what will go into your next commit

**SHA (Secure Hash Algorithm)** - an ID number for each commit

**Branch** - when a new line of development is created that diverges from the main line of development (can continue without altering the main line)


## Initializing

**git init** - sets up all of the necessary files and directories in a hidden directory called _.git_. The content of the _.git_ directory:

- _config file_ - where all project specific configuration settings are stored

- _description file_ - this file is only used by the GitWeb program, so we can ignore it

- _hooks directory_ - this is where we could place client-side or server-side scripts that we can use to hook into Git's different lifecycle events

- _info directory_ - contains the global excludes file

- _objects directory_ - this directory will store all of the commits we make

- _refs directory_ - this directory holds pointers to commits (basically the "branches" and "tags")


**git clone path new_repo** - clone an existing repo (path) into new repo


## Logging

**git status** - shows the state of our repository as Git sees it

**git log** - displays the following info about each commit: the SHA, the author, the date, the message

**git log --oneline** - a more succinct version of _git log_

**git log --stat** - displays the files that have been changed in the commit: the file(s) that have been modified, the number of lines that have been added/removed, a summary line with the total number of modified files and lines that have been added/removed

**git log -p** / **git log --patch** - displays the actual changes made to a file, different flags can be used (for example, _-w_ or _--ignore-all-space_ ignores whitespace when comparing lines)

**git log SHA** - by supplying a SHA, the _git log_ command will start at that commit

**git show** - displays the most recent commit

**git show SHA** - displays only one commit with the specified SHA, the output is exactly the same as the _git log -p SHA_: the commit, the author, the date, the commit message, the patch information. The command can be combined with the flags: _--stat_, _--patch_, _--ignore-all-space_

**git log --oneline --graph --all** - displays all branches at once in the git log output, the _--graph_ flag adds the bullets and lines to the leftmost part of the output, the _--all_ flag is what displays all of the branches in the repository


## Making commits

**git add <file1> <file2> … <fileN>** - moves files from the Working Directory to the Staging Index

**git commit -m message** - commits the changes to the repo (can be used without _-m_ flag with a code editor). The goal is that each commit has a single focus. Each commit should record a single-unit change

**git diff** - displays the changes that have been made but haven't been committed: the files that have been modified, the location of the lines that have been added/removed, the actual changes that have been made

**git tag -a tag_name** - adds a marker on a _most recent_ commit, the tag does not move around as new commits are added, the _-a_ flas creates an annotated flag (instead of a lightweight one), which includes the following info: the person who made the tag, the date the tag was made, a message for the tag

**git tag -a tag_name SHA** - adds a marker on a _specific_ commit

**git tag -d tag_name** - deletes the tag with the name _tag_name_


## Branching

**git branch** - can be used to list all branch names in the repository, create new branches, delete branches

**git branch branch_name** - creates a branch _branch_name_

**git checkout branch_name** - switches to the branch _branch_name_

**git branch -d branch_name** - deletes the branch _branch_name_ (the deletion can be forced with _-D_)

**git checkout -b branch_name** - creates a branch and switches to it all in one command


## Merging

- _merging_ is combining branches together
- making a merge makes a commit!
- two main types of merges in Git: a regular merge and a fast-forward merge
- a _fast-forward merge_ happens when one branch is ahead of another, so the merge will just move the currently checked out branch forward until it points to the same commit that the other branch, it is one of the easiest merges to do

**git merge branch_name** - merges _branch_name_ into the current (checked-out) branch, the command finds a single commit that both branches have in their commit history, combines the lines of code that were changed on the separate branches, makes a commit to record the merge, a commit message needs to be supplied (!)

**git reset --hard HEAD^** - the command to undo the merge


## Merge Conflicts

### Indicators Explanation

```
<<<<<<< HEAD everything below this line (until the next indicator) shows you what's on the current branch
||||||| merged common ancestors everything below this line (until the next indicator) shows you what the original lines were
======= is the end of the original lines, everything that follows (until the next indicator) is what's on the branch that's being merged in
>>>>>>> heading-update is the ending indicator of what's on the branch that's being merged in (in this case, the heading-update branch)
```

### Resolving A Merge Conflict

- choose which line(s) to keep
- remove all lines with indicators
- save the file(s)
- stage the file(s)
- make a commit


## Making changes

**git commit --amend** - alters the most-recent commit (change the message, add forgotten files), in order to add new files, those files should be stages as for a regular commit before running the command

**git revert SHA** - reverts a specific commit (does the exact opposite of that commit), creates a new commit with the opposite action. Resetting is different from reverting, it erases commits from the repo history completely (!)


## Relative Commit References (Ancestry References)

**^** – indicates the parent commit

**~** – indicates the first parent commit

The main difference between the ^ and the ~ is when a commit is created from a merge. A merge commit has two parents. With a merge commit, the ^ reference is used to indicate the first parent of the commit while ^2 indicates the second parent. The first parent is the branch you were on when you ran git merge while the second parent is the branch that was merged in.


Examples:

- The following indicates the parent commit of the current commit: _HEAD^_, _HEAD\~_, _HEAD\~1_

- The following indicates the grandparent commit of the current commit: _HEAD^^_, _HEAD\~2_

- The following indicates the great-grandparent commit of the current commit: _HEAD^^^_, _HEAD\~3_


## Commit messages

- do keep the message short (less than 60-ish characters)
- do explain what the commit does (not how or why!)

- do not explain why the changes are made (more on this below)
- do not explain how the changes are made (that's what git log -p is for!)
- do not use the word "and"


## Globbing and gitignore

- the *.gitignore* file is used to tell Git about the files that Git should not track, this file should be placed in the same directory that the .git directory is in

- **globbing** lets you use special characters to match patterns/characters, it is similar to regular expressions
