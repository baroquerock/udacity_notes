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

**git log --oneline --decorate --graph --all** - displays all branches at once in the git log output, the _--graph_ flag adds the bullets and lines to the leftmost part of the output, the _--all_ flag is what displays all of the branches in the repository


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



Combining branches together is called merging.

Let's see how this works, in theory. Pay attention to the two main types of merges in Git, a regular merge and a Fast-forward merge.




It's very important to know which branch you're on when you're about to merge branches together. Remember that making a merge makes a commit.

As of right now, we do not know how to undo changes. We'll go over it in the next lesson, but if you make a merge on the wrong branch, use this command to undo the merge:

git reset --hard HEAD^

(Make sure to include the ^ character! It's a known as a "Relative Commit Reference" and indicates "the parent commit". We'll look at Relative Commit References in the next lesson.)

The Merge Command
The git merge command is used to combine Git branches:

$ git merge <name-of-branch-to-merge-in>
When a merge happens, Git will:

look at the branches that it's going to merge
look back along the branch's history to find a single commit that both branches have in their commit history
combine the lines of code that were changed on the separate branches together
makes a commit to record the merge




Fast-forward Merge
In our project, I've checked out the master branch and I want _it_ to have the changes that are on the footer branch. If I wanted to verbalize this, I could say this is - "I want to merge in the footer branch". That "merge in" is important; when a merge is performed, the other branch's changes are brought into the branch that's currently checked out.

Let me stress that again - When we merge, we're merging some other branch into the current (checked-out) branch. We're not merging two branches into a new branch. We're not merging the current branch into the other branch.

Now, since footer is directly ahead of master, this merge is one of the easiest merges to do. Merging footer into master will cause a Fast-forward merge. A Fast-forward merge will just move the currently checked out branch forward until it points to the same commit that the other branch (in this case, footer) is pointing to.

To merge in the footer branch, run:





Perform A Regular Merge
Fantastic work doing a Fast-forward merge! That wasn't too hard, was it?

But you might say - "Of course that was easy, all of the commits are already there and the branch pointer just moved forward!"...and you'd be right. It's the simplest of merges.

So let's do the more common kind of merge where two divergent branches are combined. You'll be surprised that to merge in a divergent branch like sidebar is actually no different!

To merge in the sidebar branch, make sure you're on the master branch and run:

$ git merge sidebar
Because this combines two divergent branches, a commit is going to be made. And when a commit is made, a commit message needs to be supplied. Since this is a merge commit a default message is already supplied. You can change the message if you want, but it's common practice to use the default merge commit message. So when your code editor opens with the message, just close it again and accept that commit message.




Merge Conflict Indicators Explanation
The editor has the following merge conflict indicators:

<<<<<<< HEAD everything below this line (until the next indicator) shows you what's on the current branch
||||||| merged common ancestors everything below this line (until the next indicator) shows you what the original lines were
======= is the end of the original lines, everything that follows (until the next indicator) is what's on the branch that's being merged in
>>>>>>> heading-update is the ending indicator of what's on the branch that's being merged in (in this case, the heading-update branch)




Changing The Last Commit
You've already made plenty of commits with the git commit command. Now with the --amend flag, you can alter the most-recent commit.

$ git commit --amend
If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running git commit --amend will let you provide a new commit message. Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.

Add Forgotten Files To Commit
Alternatively, git commit --amend will let you include files (or changes to files) you might've forgotten to include. Let's say you've updated the color of all navigation links across your entire website. You committed that change and thought you were done. But then you discovered that a special nav link buried deep on a page doesn't have the new color. You could just make a new commit that updates the color for that one link, but that would have two back-to-back commits that do practically the exact same thing (change link colors).

Instead, you can amend the last commit (the one that updated the color of all of the other links) to include this forgotten one. To do get the forgotten link included, just:

edit the file(s)
save the file(s)
stage the file(s)
and run git commit --amend
So you'd make changes to the necessary CSS and/or HTML files to get the forgotten link styled correctly, then you'd save all of the files that were modified, then you'd use git add to stage all of the modified files (just as if you were going to make a new commit!), but then you'd run git commit --amend to update the most-recent commit instead of creating a new one



When you tell Git to revert a specific commit, Git takes the changes that were made in commit and does the exact opposite of them. Let's break that down a bit. If a character is added in commit A, if Git reverts commit A, then Git will make a new commit where that character is deleted. It also works the other way where if a character/line is removed, then reverting that commit will add that content back!



git revert <SHA-of-commit-to-revert>



	Reset vs Revert
At first glance, resetting might seem coincidentally close to reverting, but they are actually quite different. Reverting creates a new commit that reverts or undos a previous commit. Resetting, on the other hand, erases commits!

⚠️ Resetting Is Dangerous ⚠️
You've got to be careful with Git's resetting capabilities. This is one of the few commands that lets you erase commits from the repository. If a commit is no longer in the repository, then its content is gone.

To alleviate the stress a bit, Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the git reflog command. Check out these links for more info:



Relative Commit References
You already know that you can reference commits by their SHA, by tags, branches, and the special HEAD pointer. Sometimes that's not enough, though. There will be times when you'll want to reference a commit relative to another commit. For example, there will be times where you'll want to tell Git about the commit that's one before the current commit...or two before the current commit. There are special characters called "Ancestry References" that we can use to tell Git about these relative references. Those characters are:

^ – indicates the parent commit
~ – indicates the first parent commit
Here's how we can refer to previous commits:

the parent commit – the following indicate the parent commit of the current commit
HEAD^
HEAD~
HEAD~1
the grandparent commit – the following indicate the grandparent commit of the current commit
HEAD^^
HEAD~2
the great-grandparent commit – the following indicate the great-grandparent commit of the current commit
HEAD^^^
HEAD~3
The main difference between the ^ and the ~ is when a commit is created from a merge. A merge commit has two parents. With a merge commit, the ^ reference is used to indicate the first parent of the commit while ^2 indicates the second parent. The first parent is the branch you were on when you ran git merge while the second parent is the branch that was merged in.


## Commit messages

- do keep the message short (less than 60-ish characters)
- do explain what the commit does (not how or why!)

- do not explain why the changes are made (more on this below)
- do not explain how the changes are made (that's what git log -p is for!)
- do not use the word "and"




Let's say that you add 50 images to your project, but want Git to ignore all of them. Does this mean you have to list each and every filename in the .gitignore file? Oh gosh no, that would be crazy! Instead, you can use a concept called globbing.

Globbing lets you use special characters to match patterns/characters. In the .gitignore file, you can use the following:

blank lines can be used for spacing
# - marks line as a comment
* - matches 0 or more characters
? - matches 1 character
[abc] - matches a, b, _or_ c
** - matches nested directories - a/**/z matches
a/z
a/b/z
a/b/c/z


Git Ignore Recap
To recap, the .gitignore file is used to tell Git about the files that Git should not track. This file should be placed in the same directory that the .git directory is in.
