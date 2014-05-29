---
layout: lesson
root: ../..
title: Introduction to the Shell
---


### What is a shell?

* A shell is a program whose primary purpose is to read commands and run other programs.

### Why use a shell?

* High action-to-keystroke ratio
* Strong support for automating repetitive tasks
* Easily used to access and perform work on networked machines


### Which shell?

Many shells exist, and several are popular. We will use the Bourne Again Shell (BASH). It is the most popular and the most frequently found shell on Unix/Linux operating systems.


### First steps

Open your terminal and issue the following commands:

~~~
$ cd
$ git clone https://github.com/gotgenes/2014-05-29-ucsd.git
$ cd 2014-05-29-ucsd
$ pwd
~~~
{:class="in"}


#### Checkpoint

* Were you unable to find your terminal?
* Did you see this?

  ~~~
  bash: git: command not found
  ~~~
  {:class="out"}

* Did the `pwd` command output something with `2014-05-29-ucsd` at the end?

If you answered "No" to one or more of these questions, please immediately notify your instructors for assistance.


#### Aside: notation conventions

* The dollar sign `$` represents the command line prompt.
* Text formatted like this

  ~~~
  $ echo 'Hi, bash!'
  $ echo $SHELL
  ~~~
  {:class="in"}

  is input. You type this in. (Be sure to type it, do not copy-paste.)
* Text formatted like this

  ~~~
  Hi, bash!
  /bin/bash
  ~~~
  {:class="out"}

  represents output from one or more of the commands you typed in.


### Figuring out where you are

`pwd` tells you, at any point, where you're currently working in the filesystem.

`pwd` stands for "present working directory", also known as the "current working directory".


#### Aside: what's a filesystem

A filesystem is comprised of files and directories.

* Files are files, like pictures, music tracks, code, etc.
* Directories (a.k.a., "folders") contain other files and directories (called "subdirectories")


### Figuring out what's around you

`ls` lists the files and subdirectories contained in your current working directory.


#### Aside: arguments

`ls` can actually take a path (e.g., another directory) as an argument (i.e., `ls <path>`).

~~~
$ ls data
~~~
{:class="in"}

Here, "`data`" is the argument.



##### Aside: argument notation


`<a_placeholder>` indicates a placeholder for an argument (like a directory or a file).

* Do not type the angle brackets: `<` and `>`.
* Just provide the actual arguments.


##### Exercise

Compare the output of `ls` versus `ls` with an argument of your current working directory. Do you see any differences?


#### Aside: options (flags)

`ls` takes a number of options (a.k.a., flags). For example, try

~~~
$ ls -F
~~~
{:class="in"}

You can combine options and arguments. Convention is to place options first:

~~~
$ ls -F data
~~~
{:class="in"}


#### Aside: tab-completion

You can use the "Tab" key on your keyboard to help complete commands and file paths. For example try typing `pw`, then hitting the "Tab" key.

Sometimes you will need to press "Tab" twice, which will display all the possibilities.

##### Exercise

Try tab-completing paths, for example, try `ls dat` and hitting Tab. Use tab completion to help you list subdirectory contents.


### Getting help

Many commands come with their own documentation. These can usually be accessed in two ways.

* Many commands provide a `--help` flag. If you are on Linux (not OS X), try `ls --help`
* Many commands also provide a "man" page (short for "manual"). Try performing `man ls` (this will work on OS X).


#### Exercise

What does the `-a` option do for the `ls` command? Try it. Do you notice anything extra listed?


##### Aside: the `.` and `..` directories

Every directory has two special sub-directories, `.` and `..`.

* `.` points back to the directory itself
* `..` points to the directory's parent


##### Aside: absolute paths versus relative paths

Absolute paths start with the filesystem root `/`. For example, `pwd` gives the absolute path of your current working directory.

Relative paths are given relative to your current working directory. `ls data/bio` uses a path relative to the current working directory.



### Getting around (the filesystem)

Use the `cd` command to move between different directories.

* `cd ~` moves you to your home directory
* `cd` (no arguments) moves to your "home directory"
* `cd <directory>` moves you to different directories throughout the filesystem
* `cd -` moves you to the previous directory before the current one


#### Aside: the tilde (`~`)

`~` is a special character that stands for "my home directory"; BASH will interpret the tilde as such. For example, try

~~~
$ ls -F ~
~~~
{:class="in"}


#### Exercise

What directory are you in after issuing the following command?

~~~
$ cd ~/2014-05-29-ucsd/..
~~~
{:class="in"}


#### Exercise

Get back to the `2014-05-29-ucsd` using its absolute path.


### Viewing file contents

* `cat` outputs all data to the terminal
* `less` outputs to the terminal, but lets you scroll up and down
  * scroll up with the up arrow or "Page Up"
  * scroll down with the down arrow or "Page Down"
  * quit the program by pressing the "q" key on your keyboard
  * search for contents using the `/` operator
  * abandon the search using the "Escape" key


### File manipulation

* `touch <filename>` can create and empty file
* `rm` removes a file from the filesystem
* `mv` renames or moves a file from one location to another
* `mkdir` makes a directory
* `rmdir` removes a directory if it's empty


#### Aside: globbing

BASH interprets the asterisk "`*`" character as a wildcard. It matches one or more characters.

##### Exercise

1. Use touch to create five empty files with numbers as file names (e.g., `touch 1.num`).
1. Use globbing to list all files with a `.num` extension.
1. Use globbing to remove all files with a `.num` extension.


### File processing

* `wc` can count the number of bytes (characters), words, and lines in a file
* `cut` can extract one or more columns from regularly structured data
* `head` can give the first few lines of a file
* `tail` can give the last few lines of a file
* `sort` can re-order the contents of a file
* `uniq` will eliminate contiguous redundant lines


#### Aside: output redirection

The `>` character is used to redirect output to a file.

The `|` ("pipe") character is used to redirect output to another program.


### Viewing differences between files

`diff <file1> <file2>` is a tool that can display differences between two files. Frequently you will want to use `diff` with the `-u` flag (i.e., use `diff -u <file1> <file2>`.


### Additional Resources

* Zed Shaw's [The Command Line Crash Course](http://cli.learncodethehardway.org/book/)
* Chris Lasher's [Shell Basics Series](http://showmedo.com/videotutorials/series?name=pQZLHo5Df)

