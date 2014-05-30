---
layout: lesson
root: ../..
title: "Version Control With Git: Local Operations"
---
## Automatically merging changes with git 

Yesterday we showed you how you could use version control to record
the history of changes to files and rewind files to their old revisions.

Today we will cover combining different sets of changes (that may have
been made at different times, by different people, or for different 
purposes.)  When it's possible to apply both your changes and your collaborator's
changes without the two interfering with each other, git can combine both
sets of changes automatically.  


Let's go back to our repository-- 
    cd ~/my_first_repository
And admire our work from yesterday:

    git log --oneline

## git branch : Listing, Creating, and Deleting Branches

Branches are pointers to a version of a repository that can be edited and
version controlled in parallel. They are useful for pursuing various
implementations experimentally or maintaining a stable core while
developing separate sections of a code base.

Without an argument, the **branch** command lists the branches that
exist in your repository.

    $ git branch
    * master

The master branch is created when the repository is initialized. With an
argument, the **branch** command creates a new branch with the given
name.

    $ git branch experimental
    $ git branch
    * master
      experimental

To delete a branch, use the **-d** flag.

    $ git branch -d experimental
    $ git branch
    * master

## git checkout : Switching Between Branches, Abandoning Local Changes

The **git checkout** command allows context switching between branches
as well as abandoning local changes.

To switch between branches, try

    $ git branch newbranch 
    $ git checkout newbranch 
    $ git branch

How can you tell we've switched between branches? When we used the
branch command before there was an asterisk next to the master branch.
That's because the asterisk indicates which branch you're currently in.

## git merge : Merging Branches

At some point, the experimental branch may be ready to become part of
the core or two testing branches may be ready to be combined for further
integration testing. The method for combining the changes in two
parallel branches is the **merge** command.

### Exercise : Create and Merge Branches

Step 1 : Create two new branches and list them

    $ git branch first
    $ git branch second

Step 2 : Make changes in each new branch and commit them.

    $ git checkout first
    Switched to branch 'first'
    $ touch firstnewfile
    $ git add firstnewfile
    $ git commit -am "Added firstnewfile to the first branch."
    [first 68eba44] Added firstnewfile to first branch.
     0 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 firstnewfile
    $ git checkout second
    Switched to branch 'second'
    $ touch secondnewfile
    $ git add secondnewfile
    $ git commit -am "Added secondnewfile to the second branch."
    [second 45dd34c] Added secondnewfile to the second branch.
     0 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 secondnewfile

Step 3 : Merge the two branches into the core

    $ git checkout first
    Switched to branch 'first'
    $ git merge second
    Merge made by recursive.
     0 files changed, 0 insertions(+), 0 deletions(-)
      create mode 100644 secondnewfile
    $ git checkout master
    Switched to branch 'master'
    $ git merge first
    Updating 1863aef..ce7e4b5
    Fast-forward
     0 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 firstnewfile
     create mode 100644 secondnewfile

## Resources

[git book](http://git-scm.com/book)
