# Version control

## Terminology

**Version Control System (VCS)** / **Source Code Manager (SCM)** - a tool that manages different versions of source code

**Commit** - a snapshot of the state of a project (like a save point in a game)

**Repository** - a directory which contains your project work (made up of commits)

**Checkout** - when content in the repository has been copied to the Working Directory

**Staging Area** / **Staging Index** / **Index** - a file in the Git directory that stores information about what will go into your next commit

**SHA (Secure Hash Algorithm)** - an ID number for each commit

**Branch** - when a new line of development is created that diverges from the main line of development (can continue without altering the main line)


## Commands


**git init** - sets up all of the necessary files and directories in a hidden directory called _.git_. The content of the _.git_ directory:

- _config file_ - where all project specific configuration settings are stored

- _description file_ - this file is only used by the GitWeb program, so we can ignore it

- _hooks directory_ - this is where we could place client-side or server-side scripts that we can use to hook into Git's different lifecycle events

- _info directory_ - contains the global excludes file

- _objects directory_ - this directory will store all of the commits we make

- _refs directory_ - this directory holds pointers to commits (basically the "branches" and "tags")



**git clone path new_repo** - clone an existing repo (path) into new repo

**git status** - shows the state of our repository as Git sees it

**git log** - displays the following info about each commit: the SHA, the author, the date, the message

**git log --oneline** - a more succinct version of _git log_

**git log --stat** - displays the files that have been changed in the commit: the file(s) that have been modified, the number of lines that have been added/removed, a summary line with the total number of modified files and lines that have been added/removed

**git log -p** / **git log --patch** - displays the actual changes made to a file

**-w** / **--ignore-all-space** - ignore whitespace when comparing lines

**git log SHA** - by supplying a SHA, the _git log_ command will start at that commit

**git show** - displays the most recent commit

**git show SHA** - displays only one commit with the specified SHA, the output is exactly the same as the _git log -p SHA_: the commit, the author, the date, the commit message, the patch information. The command can be combined with the flags: _--stat_, _--patch_, _--ignore-all-space_




TIP: Did you also notice the helpful text that's located just beneath "Changes to be committed"? It says (use "git rm --cached <file>..." to unstage) This is a hint of what you should do if you accidentally ran git add and gave it the wrong file.

As a side note, git rm --cached is not like the shell's rm command. git rm --cached will not destroy any of your work; it just removes it from the Staging Index.

Also, this used the word "unstage". The act of moving a file from the Working Directory to the Staging Index is called "staging". If a file has been moved, then it has been "staged". Moving a file from the Staging Index back to the Working Directory will unstage the file. If you read documentation that says "stage the following files" that means you should use the git add command.


Git Add Recap
The git add command is used to move files from the Working Directory to the Staging Index.

$ git add <file1> <file2> … <fileN>
This command:

takes a space-separated list of file names
alternatively, the period . can be used in place of a list of files to tell Git to add the current directory (and all nested files)



Bypass The Editor With The -m Flag
TIP: If the commit message you're writing is short and you don't want to wait for your code editor to open up to type it out, you can pass your message directly on the command line with the -m flag:

$ git commit -m "Initial commit"
In the example above, the text "Initial commit" is used as the commit message. Be aware that you can't provide a description for the commit, only the message part.


The goal is that each commit has a single focus. Each commit should record a single-unit change. Now this can be a bit subjective (which is totally fine), but each commit should make a change to just one aspect of the project.


Git Commit Recap
The git commit command takes files from the Staging Index and saves them in the repository.

$ git commit
This command:

will open the code editor that is specified in your configuration
(check out the Git configuration step from the first lesson to configure your editor)
Inside the code editor:

a commit message must be supplied
lines that start with a # are comments and will not be recorded
save the file after adding a commit message
close the editor to make the commit
Then, use git log to review the commit you just made!

Do

do keep the message short (less than 60-ish characters)
do explain what the commit does (not how or why!)
Do not

do not explain why the changes are made (more on this below)
do not explain how the changes are made (that's what git log -p is for!)
do not use the word "and"
if you have to use "and", your commit message is probably doing too many changes - break the changes into separate commits
e.g. "make the background color pink and increase the size of the sidebar"

Explain the Why
If you need to explain why a commit needs to be made, you can!

When you're writing the commit message, the first line is the message itself. After the message, leave a blank line, and then type out the body or explanation including details about why the commit is needed (e.g. URL links).

Here's what a commit message edit screen might look like:

Git Diff Recap
To recap, the git diff command is used to see changes that have been made but haven't been committed, yet:

$ git diff
This command displays:

the files that have been modified
the location of the lines that have been added/removed
the actual changes that have been made



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





CAREFUL: In the command above (git tag -a v1.0) the -a flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. git tag v1.0) then it'll create what's called a lightweight tag.

Annotated tags are recommended because they include a lot of extra information such as:

the person who made the tag
the date the tag was made
a message for the tag
Because of this, you should always use annotated tags.


Git Log's --decorate Flag
As you've learned, git log is a pretty powerful tool for letting us check out a repository's commits. We've already looked at a couple of its flags, but it's time to add a new one to our toolbelt. The --decorate flag will show us some details that are hidden from the default view.

Try running git log --decorate now!


In the 2.13 update to Git, the log command has changed to automatically enable the --decorate flag. This means that you do not need to include the --decorate flag in your command, since it is automatically included, anyway! So the following commands result in the exact same output:

Deleting A Tag
What if you accidentally misspelled something in the tag's message, or mistyped the actual tag name (v0.1 instead of v1.0). How could you fix this? The easiest way is just to delete the tag and make a new one.

A Git tag can be deleted with the -d flag (for delete!) and the name of the tag:

$ git tag -d v1.0


Adding A Tag To A Past Commit
Running git tag -a v1.0 will tag the most recent commit. But what if you wanted to tag a commit that occurred farther back in the repo's history?

All you have to do is provide the SHA of the commit you want to tag!

$ git tag -a v1.0 a87984
(after popping open a code editor to let you supply the tag's message) this command will tag the commit with the SHA a87084 with the tag v1.0. Using this technique, you can tag any commit in the entire git repository! Pretty neat, right?...and it's just a simple addition to add the SHA of a commit to the Git tagging command you already know.


Git Tag Recap
To recap, the git tag command is used to add a marker on a specific commit. The tag does not move around as new commits are added.

$ git tag -a beta
This command will:

add a tag to the most recent commit
add a tag to a specific commit if a SHA is passed



The git branch command
The git branch command is used to interact with Git's branches:

$ git branch
It can be used to:

list all branch names in the repository
create new branches
delete branches



Create A Branch
To create a branch, all you have to do is use git branch and provide it the name of the branch you want it to create. So if you want a branch called "sidebar", you'd run this command:

$ git branch sidebar




The git checkout Command
Remember that when a commit is made that it will be added to the current branch. So even though we created the new sidebar, no new commits will be added to it since we haven't switched to it, yet. If we made a commit right now, that commit would be added to the master branch, not the sidebar branch. We've already seen this in the demo, but to switch between branches, we need to use Git's checkout command.

$ git checkout sidebar



Branches In The Log
The branch information in the command prompt is helpful, but the clearest way to see it is by looking at the output of git log. But just like we had to use the --decorate flag to display Git tags, we need it to display branches.

$ git log --oneline --decorate


Delete A Branch
A branch is used to do development or make a fix to the project that won't affect the project (since the changes are made on a branch). Once you make the change on the branch, you can combine that branch into the master branch (this "combining of branches" is called "merging" and we'll look at it shortly).

Now after a branch's changes have been merged, you probably won't need the branch anymore. If you want to delete the branch, you'd use the -d flag. The command below includes the -d flag which tells Git to delete the provided branch (in this case, the "sidebar" branch).

$ git branch -d sidebar


To force deletion, you need to use a capital D flag - git branch -D sidebar


Git Branch Recap
To recap, the git branch command is used to manage branches in Git:

# to list all branches
$ git branch

# to create a new "footer-fix" branch
$ git branch footer-fix

# to delete the "footer-fix" branch
$ git branch -d footer-fix
This command is used to:

list out local branches
create new branches
remove branches




But did you know that the git checkout command can actually create a new branch, too? If you provide the -b flag, you can create a branch and switch to it all in one command.

$ git checkout -b richards-branch-for-awesome-changes
It's a pretty useful command, and I use it often.





See All Branches At Once
We've made it to the end of all the changes we needed to make! Awesome job!

Now we have multiple sets of changes on three different branches. We can't see other branches in the git log output unless we switch to a branch. Wouldn't it be nice if we could see all branches at once in the git log output.

As you've hopefully learned by now, the git log command is pretty powerful and can show us this information. We'll use the new --graph and --all flags:

$ git log --oneline --decorate --graph --all
The --graph flag adds the bullets and lines to the leftmost part of the output. This shows the actual branching that's happening. The --all flag is what displays all of the branches in the repository.




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



