---
layout: lesson
root: ../..
title: Introduction to Version Control with Git
---

## Version Control


### Why use version control?

Have you ever

* Had scripts with names like
  `critical_analysis_pipeline-victorias_copy-rewrite3-no_comma_output.pl`?
* Had code that used to work and now it doesn't?
* Found yourself unable to reproduce a six month-old analysis because you
  can't get the code from six months ago?
* Accidentally overwritten changes you made to the code?
* Accidentally overwritten changes someone else made to code?
* Wanted to make your process transparent to others?
* Wanted a way to share code easily?
* Wanted to know who made what changes and when they made them?

Version control solves all these problems.


### What is version control?

* Tracks changes to files over time
* Restores files to any previous state
* Allows multiple people to make changes simultaneously


### What is Git?

* Git is a version control system (VCS) – software that performs all the
  tasks of version control
* Git is a distributed version control system – it stores metadata and
  content together; most operations require no Internet connectivity
* Provides commands to record changes, query about past changes, and
  incorporate collaborator's changes with your own.


### Before starting

Tell Git a little bit about yourself and your preferences. In a
terminal, enter the following:

~~~
$ git config --global user.name "<your_name>"
$ git config --global user.email "<your_email_address>"
$ git config --global color.ui auto
$ git config --global core.editor "<your_text_editor_of_choice>"
~~~
{:class="in"}

For example,

~~~
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
$ git config --global core.editor "nano"
~~~
{:class="in"}


### Getting help

Git provides its own set of documentation:

~~~
$ git help
~~~
{:class="in"}

Any time you need to learn or remember details of a particular command, issue

~~~
$ git help <command>
~~~
{:class="in"}

For example

~~~
$ git help help
~~~
{:class="in"}

gives the details on the `git help` command.


#### Exercise

You will encounter a lot of jargon with Git. Git's built-in documentation
includes a glossary of terms in the form of a "guide". Find this
glossary using `git help`.


### Creating (initializing) your repository

~~~
$ cd ~
$ mkdir my_first_repo
$ cd my_first_repo
$ git init
~~~


### What is a repository?

A repository tracks changes to files contained within the repository.

A repository is comprised of:

1. a top level directory (ours is `~/my_first_repo`),
1. a `.git` subdirectory containing all repository data,
1. a set of files and subdirectories contained within the top level directory


## Tracking changes


### Overview of the layers of a Git repository

![The layers of a Git repository](img/local_git_areas.png)

* Working directory: the files and subdirectories as they exist on your
  file system this very moment
* Staging area (a.k.a., "staging index", or just "index"): a collection
  of changes specified to recording upon next commit
* Commit history [labeled "git directory (repository)" above]:
  a collection of commits (snapshots) containing the entire history of
  changes since the repository was initialized

The majority of Git commands let us do one of two things:

1. Determine what's different between any of the three layers.
1. Flow those differences between any layer to any other layer.

Most of the time, we will flow changes from working directory → staging
index → commit history.


### Determining the state of your repository and its files

`git status` informs you of the state of the repository and the files
within it. It reports the following information:

* What branch you currently have checked out. (More on branches later.)
* Whether your local copy of a branch is in sync with a remote copy.
  (More on remote repositories later.)
* Whether or not any files have changes, specifically:
  * "working directory clean": you have no outstanding changes
  * "Changes not staged for commit": lists files with changes since the
    most recent commit on your current branch; these changes won't be
    recorded by in the next commit unless you stage them
  * "Changes to be committed": lists files with changes you have staged
    to be recorded in the next commit
* Whether or not you have any conflicts that require resolution. (More
  on merge conflicts later.)
* Whether or not you are in the middle of another Git operation.
* Helpful suggestions on what Git commands you might consider using
  next.


### File life cycle and status

The following diagram presents a view centric to the status of an
individual file.

![File lifecycle in Git](img/git_file_lifecycle.png)

* Untracked: the file exists in the working directory but Git does not
  track changes to it.
* Unmodified: the file is in the same state in the working directory
  as it was last committed
* Modified: the file has changes since


### Telling Git to track a file


* `git add <untracked_file>` tells git to begin tracking a file; the
  the command changes file status from "untracked" to "staged" (verify
using ``git status``)
* **NOTE**: Git does not track any given file until explicitly
  told to do so with `git add`.


### Committing your changes (making snapshots)

* `git commit` makes a new snapshot of the state of files in the
  based on changes "staged" with `git add` prior to issuing `git commit`
* Unstaged changes will not be committed, but can be staged for a later
  commit.
* `git commit` changes file status from "staged" to "unmodified"
* `git commit` opens the editor you specified as `core.editor` during
  configuration; write an informative message about the commit, save the
  message, and close the file.
* For smaller commits that need only a brief explanation, use the `-m`
  flag, as in

  ~~~
  $ git commit -m "A short but informative statement."
  ~~~
  {:class="in"}


#### Exercise

Why does `git commit` change file status to "unmodified"? Does this mean
it discarded the changes?


#### Exercise

What happens if you attempt to perform `git commit` immediately after
performing a `git commit`?


#### Aside: Commit message DOs and DON'Ts

* Do make your commit messages informative; the more informative, the more
  you help others, and more importantly, your future (forgetful) self.
* Do make the first sentence a short (~50-60 character) summary of the
  changes committed.
* Do separate your first sentence from remaining sentences, as its own
  paragraph.
* Do use following paragraphs to go into more depth about changes.
* Do try to keep individual commit message lines to 70-80 characters
  maximum (usually requires configuration settings in your editor).
* Do try to proofread your commit message before closing the file. The
  commit message is considered part of the commit.  Altering messages
  after committing is frowned upon at best and can break your
  repository history at worst.
* Don't go into fine details of the changes; Git provides tools to view
  the specific changes for any given commit. (See `git show` and `git
  diff` later.)


#### Aside: creating an alias for `commit`

Typing `git commit` takes effort. Make your computer reduce your effort by
creating an alias of `git ci`.

~~~
$ git config --global alias.ci 'commit'
~~~
{:class="in"}

Typing two characters is a lot easier!


### Modifying a file

* Change a tracked file in the working directory changes the status
  from "unmodified" to "modified"
* `git add <modified_file>` stages the changes to the staging index and
  changes the file status from "modified" to "staged"


#### Exercise

What happens if you modify a file that you have already staged? What is
the status of that file: "unmodified", "modified", or "staged"?


### Seeing what's changed

`git diff` shows the *unstaged* changes of tracked files versus the
  most recent commit.

* Changes are shown in unified diff format, similar to the command line
tool `diff -u`.
* `-` indicates an line that was removed from the file
* `+` indicates a new line that was added to the file
* a line that was modified will be represented as one `-` line
followed by one `+` line
* if multiple lines were modified, they will be represented as one
block of `-` lines followed by a block of `+` lines

#### Exercise

How would you view changes that are already staged but not yet
committed? Confirm by making changes, staging them with `git add`, and
viewing these staged changes.


## Undoing changes


### Discarding changes to a file

`git checkout -- <modified_file>` discards changes to the modified
file and changes the status back to "unmodified".

**NOTE**: changes will be discarded forever; use with caution!


#### Aside: the `--` argument

The argument of two dashes (`--`) provided to `git checkout` above tells
the command, "All following arguments are file paths." The `--` argument
is optional, but highly recommended. It is used to disambiguate revision
specification arguments (e.g., branch names and tags) from file path
arguments.

We will cover several Git commands which accept `--` as an argument for
disambiguation, including:

* `git checkout`
* `git reset`
* `git log`
* `git diff`


### Removing and untracking files

`git rm` removes a file from the filesystem and stages for removal from
the set of files tracked by the repository.

`git rm --cached` will only stage the file to be untracked by the
repository, but will leave the file on the filesystem.


#### Exercise

What happens if you remove a tracked file from disk with `rm <tracked_file>`
(not `git rm`, but the `rm` from your shell)?  What does `git status` say?

Suppose we accidentally remove a tracked file from disk. Does Git have a
command to restore the accidentally-removed file?


### Unstaging changes from the index

`git reset -- <staged_file>` unstages changes staged in the index for a
particular file; it changes file status from "staged" to "modified".

#### Exercise

Take a file in your repository through all the file statuses and back:

1. Untracked to tracked (don't forget to commit)
1. Unmodified to modified.
1. Modified to staged.
1. Staged back to modified.
1. Modified back to unmodified.
1. Unmodified to untracked.

#### Exercise

Use a combination of `git reset` and `git checkout` to undo a `git rm`
(do not commit the `git rm`).


### Undoing (reverting) committed changes


## Working with repository history


### Viewing history with `git log`


### Viewing differences between commits with `git diff`


## Branching and merging


### Viewing available branches


### Creating a new branch


### Switching between branches


### Merging changes from one branch into another


### Resolving merge conflicts


### Additional resources

* [Pro Git](http://git-scm.com/book/) (a.k.a. "The Git Book")
* [An interactive Git Cheatsheet](http://ndpsoftware.com/git-cheatsheet.html)
* [A Visual Git Reference](http://marklodato.github.io/visual-git-guide/index-en.html)
* [Visualizing Git Concepts with D3](http://www.wei-wang.com/ExplainGitWithD3/)
* [GitHub Help](http://help.github.com) (help.github.com)
* [Learn Git Branching](http://pcottle.github.io/learnGitBranching/)
* [Chris Lasher's .gitconfig](http://bit.ly/1b2aNkv)


