---
title: Shell Tutorial for Absolute Beginners
add_to_head: <link rel="stylesheet" type="text/css" href="asciinema-player.css" />
---

# 0. Artillery Preparation

The shell (or the command line) is where you enter commands. Though it may appear scary at first sight, it is a very powerful tool that allows you to do much more than any graphical interface would. This tutorial aims to make you comfortable in the shell, assuming no previous knowledge.

This tutorial makes generous use of [asciinema](https://asciinema.org/): it is full of "videos" (not really videos) of what it looks like to type the commands I will be talking about. You can pause and replay everything, and because it is actually text, you can copy things from the window. Look:

<asciinema-player src="cast/asciinema-demo.cast" data-speed="2" ></asciinema-player>

We will be using the Friendly Interactive shell -- `fish`. You can install it with your package manager, either a graphical one, or by typing the commands:

* `pkg install fish` on FreeBSD
* `brew install fish` on OS X
* `apt-get install fish` on Debian-based Linux

Afterwards, you can run it inside your usual shell by typing `fish`.

This is what the process looks like on FreeBSD:

<asciinema-player src="cast/install-fish.cast" data-speed="2"></asciinema-player>

## An appetizer: A bit of fishy awesomeness

Notice that Fish suggests things you might want to type, and the predictions get better over time. Just press the right arrow to accept the suggestion. This does not immediately execute the command, you can still edit it, so do not be afraid to press right arrow a lot :-)

# 1. Moving around the filesystem

## Basics

Similarly to Windows, files on Unix-like systems are arranged in directories (folders). 

You can use the `cd` (change directory) command to go to a directory, and the `ls` command to list the contents of a directory:

<asciinema-player src="cast/cd-ls.cast" data-speed="2"></asciinema-player>

As you probably noticed, your shell knows which directory you are in currently, and `cd` tells it to change it. Many commands (such as `ls`) will work in the current directory unless told otherwise.

The *shortened* path to the current directory is displayed in the command prompt: if you see e.g. `kamila@mymachine ~/M/Album2>`, you know you are in the directory `Album2`, which is inside something that begins with an M (in this case `Music`). The `~` stands for your home directory. (The first part of the prompt is your username and hostname.)

Unlike on Windows, all files are arranged in a single file tree (not in separate trees for `C:\`, `D:\`, etc.).
The top of the file tree is called `/`. (This is like `C:\` on Windows, except there is no `D:\`.) The character used to separate directories in paths is a `/` (Windows uses `\` for the same thing).

You can specify files and directories either relative to the current directory, like above, or with an absolute (i.e. full) path -- starting at the top, with a `/`.

The command `pwd` **p**rints **w**orking (i.e. current) **d**irectory.

<asciinema-player src="cast/rel-and-abs-paths.cast" data-speed="2"></asciinema-player>

## Creating and modifying files

Start by going to `/tmp` (directory for temporary files), because that's where you can't do much damage :-)

Some useful commands are:

* `mkdir`: make directory
* `echo`: just prints everything you give it, which sounds useless, but...
* `>` is a special character that tells the shell to write things into files instead of on the screen
* so `echo hello world > hello.txt` will write "hello world" into a file called `hello.txt`
* `cat` prints file contents into the terminal

<asciinema-player src="cast/rel-and-abs-paths.cast" data-speed="2"></asciinema-player>

### Bonus: Some more useful file-related commands

* `less` lets you scroll in big files (quit with `q`):
<!--<asciinema-player src="cast/more-file-commands-less.cast" data-speed="2"></asciinema-player>-->
* `tree` prints the file tree (you may need to install it first)
<!--<asciinema-player src="cast/more-file-commands-tree.cast" data-speed="2"></asciinema-player>-->
* `rmdir` removes an empty directory
<!--<asciinema-player src="cast/more-file-commands-rmdir.cast" data-speed="2"></asciinema-player>-->
* `cp -a` copies a directory and all its contents.  
* `rm -r` removes a directory and all its contents.
<!--<asciinema-player src="cast/more-file-commands-cprm.cast" data-speed="2"></asciinema-player>-->
* `ls -l` shows more info about the files, like when it was changed or file size; add `-h` to show human-readable file sizes
<!--<asciinema-player src="cast/more-file-commands-ll.cast" data-speed="2"></asciinema-player>-->

# Awesome fish sauce

Fish has some very helpful features. Here are the most useful ones.

Note: This is difficult to explain when you don't see which exact keys I am pressing. Go try it yourself!

## Tab completion

You can press the Tab key to autocomplete commands or files at any time. If there is a unique completion, fish will complete it; if not, it will list the options. If you press Tab multiple times, it will cycle through possible options; press Enter to accept a completion. 

<asciinema-player src="cast/tab-completion-1.cast" data-speed="2"></asciinema-player>

You can search among the possible completions (after pressing Tab at least twice) by simply starting to type when the options are displayed; type Enter to accept a completion. A combination of typing to filter and tabbing to cycle through options can get you to what you want very quickly with a bit of practice. Just don't forget to accept the completion when you are happy by pressing Enter.

<asciinema-player src="cast/tab-completion-search.cast" data-speed="2"></asciinema-player>

Fish is quite smart and will try to tab complete things even if they are not an exact match. This is useful e.g. when you make a typo or when you don't remember the exact file name. Play with it!

### Tab completion is quite magic

As mentioned, Tab can complete all sorts of things. Importantly, it can complete commands; and it provides short descriptions of what each command does. This is great if you can't remember exactly which command you are looking for:
<asciinema-player src="cast/tab-completion-commands.cast" data-speed="2"></asciinema-player>

Some important commands are so important that Fish knows more about them; in that case, it can complete the arguments too:
<asciinema-player src="cast/tab-completion-commands-args.cast" data-speed="2"></asciinema-player>

## Using previously typed commands

When doing things in the shell, you often need to run the same or similar command several times; or you do several things with the same file; or similar. Fish lets you save time in such cases by letting you search the command history by pressing the up arrow.

If you just press Up without typing anything, it will go through the previous commands. If you type something and then press Up, it will go through only those commands which contain the characters you had typed. You can also press Down to go to more recent commands, of course.

<asciinema-player src="cast/history.cast" data-speed="2"></asciinema-player>

If you want to go through the previous *words* you had typed, instead of whole commands, just use Alt+Up instead. This also works with the searching: typing a few letters and then pressing Alt+Up will go through only matching words.

<asciinema-player src="cast/history-alt-1.cast" data-speed="2"></asciinema-player>

You will often do several things with the same file: for this, just type your command and then press Alt+Up once to find the previous file name again:

<asciinema-player src="cast/history-alt-2.cast" data-speed="2"></asciinema-player>

<!--
# TODO things

 You can also set it as your default shell for your user (but NOT for root) with `chsh -s fish` (on less smart systems, you may need to tell it something like `/usr/bin/fish`).
 -->

<script src="asciinema-player.js"></script>