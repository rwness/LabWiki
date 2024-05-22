---
title: "TheNessLab : Bash Reference"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Coding tips and tutorials](Coding-tips-and-tutorials_11436186.html)
:::

# [ TheNessLab : Bash Reference ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Ahmed Raza Hasan]{.author}, last modified on Jun 01, 2017
:::

::: {#main-content .wiki-content .group}
(\*\*\* under construction - turn back now, and have your mortal life
spared \*\*\*)

The bash shell is a highly useful means of interacting with your
computer (or, in the case of our server, *a* computer). We all use the
bash shell in order to get our Jupyter Notebooks set up and perhaps run
some command line programs, but turns out it can do a lot more past
that! 

Understanding even basic Unix commands can go a really long way,
especially in a genomics environment where the inputs are big and the
outputs can be bigger. Working with large text files in particular is a
breeze with said tools where something like Python or R would struggle
to even load them in. Finally, bash is incredibly powerful when it comes
to automating tasks with ease.

A quick glossary:

-   stdin = input. this is what you are entering into the command line
-   stdout = output. this is what gets printed to the console after
    something is run

## fundamentals {#BashReference-fundamentals}

`pwd` - prints current directory to stdout

-   the current directory you are in determines what bash \'immediately
    sees\' when you, say, call upon a file
    -   if this makes no sense, I promise it will soon enough

`whoami` - in case of identity crisis

`ls` - lists files in current directory

-   super useful!
-   like most Unix commands, can be altered with *flags*
    -   flags are instantiated using a single hyphen (-), and almost
        always consist of just one letter
    -   caveat - sometimes flags are entire words, and start with two
        dashes
        (ie [\--flag]{style="font-family: monospace;"}[)]{style="font-family: Arial , sans-serif;"}[ ]{style="font-family: monospace;"}but
        you likely won\'t see these as often
-   for instance, `ls -l` will return files in the directory in a list
    format, while `ls -t` lists them in descending order since they were
    last modified
-   multiple flags can be used at once, either as `ls -l -t` or just
    `ls -lt`

`man` - pull up the help page for a command

-   did you forget the `ls` flags already?
-   well, no sweat - running `man ls` will pull up a handy reference
-   scroll up and down with the arrow keys, and press q to exit the man
    (manual) page

`cd` - change directory

-   switches working directory to specified folder
-   for instance, `cd Desktop/` will take me to a folder called
    [Desktop/]{style="font-family: monospace;"},
    *assuming *`Desktop/ `*is in my current directory*
-   obviously this isn\'t always the case - but to go back a folder, use
    `cd .. `or [cd ../]{style="font-family: monospace;"}
    -   this can be chained together using forward slashes - for
        instance, `cd ../../` will go back two folders up in the
        hierarchy (i.e. from `/scratch/research/projects` to
        `/scratch/`)
-   if the path given to cd starts at the root directory, then bash
    won\'t complain about being given a folder that\'s not in your
    current working directory
    -   for instance, I can do `cd /scratch/research/references` even if
        I\'m currently in `scratch/research/projects/chlamydomonas`, as
        long as I write out the full path

`echo` - prints input back to stdout

-   bash\'s equivalent of `print()`, really
-   `echo hello there` will return `hello there`
-   inputs don\'t \*have\* to be in quotes, but bash won\'t mind if you
    do wrap them with either single or double quotes

## basic file operations {#BashReference-basicfileoperations}

`cat` - print contents of file

-   `cat <file>` will simply return the contents of the file to stdout
-   however, `cat` can take multiple files as arguments, and
    will *concatenate *them before printing to stdout
-   for instance, `cat <file1> <file2>` will return the entire contents
    of both file1 and file2 one after the other
-   this is useful for quickly combining large flat files containing
    data, and synergizes super well with pipe operations (more on that
    in the tips and tricks article)

`mkdir` - creates a new folder

-   `mkdir myfolder` will create an empty folder called `myfolder` in
    your current working directory
-   `mkdir folder1 folder2` will make two folders named `folder1` and
    `folder2` respectively

`mv` - move files around/rename files

-   `mv file.txt data/files` will move `file.txt` to `/data/files`
-   adding the `-v` flag (i.e. `mv -v`) is especially useful, as bash
    will explicitly print out what it\'s moving and where
-   `mv` works well with *wildcards* in moving several files around -
    more on that later on as well
-   finally, `mv` also allows us to rename files by \'moving\' a file on
    top of itself
    -   for instance, `mv file.txt my_file.txt` will rename `file.txt`
        to `my_file.txt`

`rm` - delete things

-   this is a frighteningly efficient command, and **has no undo
    button**
-   in Unix, there is no Recycle Bin for deleted files to go to - they
    are promptly sent to the void and you will never, ever see them
    again. you hear that? **never.**
-   `rm -i` will prompt for confirmation before you delete something, so
    it might be good to make a habit of that
-   `rm` will complain if you make it delete a folder, but that can be
    bypassed with `rm -rf`
-   possibly goes without saying, but be extremely careful when using
    `rm` on multiple files at once!

`rmdir` - delete a folder

-   an alternative to the scarier `rm -rf` if you feel like it

## slightly less basic file operations {#BashReference-slightlylessbasicfileoperations}

chmod

head

tail

less

sort

wc

gzip

## operators {#BashReference-operators}

pipe

`>`

`>>`

`!$`

`!!`

## loops {#BashReference-loops}

## parallel operations {#BashReference-paralleloperations}

## vi 101 {#BashReference-vi101}

## something about tmux? {#BashReference-somethingabouttmux?}

\

\

\
:::
:::
:::

::: {#footer role="contentinfo"}
::: {.section .footer-body}
Document generated by Confluence on May 22, 2024 11:44

::: {#footer-logo}
[Atlassian](https://www.atlassian.com/)
:::
:::
:::
:::
