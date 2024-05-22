---
title: "TheNessLab : Useful .bash_profile settings"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Coding tips and tutorials](Coding-tips-and-tutorials_11436186.html)
:::

# [ TheNessLab : Useful .bash_profile settings ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ James Santangelo]{.author}, last modified on Apr 29, 2017
:::

::: {#main-content .wiki-content .group}
The .*bash_profile* is a shell configuration file that is executed every
time you start a login shell. This is the case anytime you are prompted
for your username and password prior to the start of the shell (e.g.
logging in to a remote server via ssh). This config file is executed
just prior to the bash prompt appearing in the shell and allows you to
more finely tune your shell environment. This page will first go over
how to create your own .*bash_profile* config file on hpcnode1 and then
serve as a repo for useful aliases and functions that folks have used to
make their lives just a little easier while computing. Feel free to add
aliases, functions or other commands to the lists below. Also, Here is a
screenshot of a *.bash_profile *configuration file. 

[[![](attachments/11436107/11436104.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/11436107/11436104.png"
unresolved-comment-count="0" linked-resource-id="11436104"
linked-resource-version="2" linked-resource-type="attachment"
linked-resource-default-alias="Screen Shot 2017-04-28 at 11.15.20 PM.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="11436107"
linked-resource-container-version="2"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}](attachments/11436107/11436104.png){linked-resource-id="11436104"
linked-resource-version="2" linked-resource-type="attachment"
linked-resource-default-alias="Screen Shot 2017-04-28 at 11.15.20 PM.png"
nice-type="Image" linked-resource-content-type="image/png"
linked-resource-container-id="11436107"
linked-resource-container-version="2"}

## Creating a .*bash_profile* configuration file {#Useful.bash_profilesettings-Creatinga.bash_profileconfigurationfile}

1.  ## [Make sure you are in your home directory (i.e. /home/user).]{style="font-size: 14.0px;"} {#Useful.bash_profilesettings-Makesureyouareinyourhomedirectory(i.e./home/user).}

2.  Create the .*bash_profile* config file (assuming it doesn\'t exit)
    using the text editor of your choice. Vim is a good choice. At the
    command line, type                      `vi .bash_profile. `

3.  Exit the .*bash_profile* file by typing  `:wq`

4.  Type   l`s -al`.   You should now have an empty .*bash_profile* file
    in your home directory

## Useful settings to place in your .*bash_profile* configuration file {#Useful.bash_profilesettings-Usefulsettingstoplaceinyour.bash_profileconfigurationfile}

### Run upon login {#Useful.bash_profilesettings-Runuponlogin}

The first thing I added to my configuration file was a single line that
automatically changes to my project folder upon login. This is useful
since this is where most of the action happens for me on the server and
this avoids me having the move there every time I login. Add the
following line to your .*bash_profile* file:

[`cd /path/to/directory/ >& /dev/null`]{.s1}

Now, every time you login the above command will be read from
.*bash_profile* and you will appear in your folder of choice with a bash
prompt. Of course, you have to change `/path/to/directory/` with the
path to the folder you wish to move to. The `>& /dev/null` at the end of
line is likely unnecessary but is good practice in some cases. It
redirect both STDERR (i.e. warnings and errors) and STDOUT (i.e. output)
to `/dev/null/` (i.e. the directory on Linux machines where things go to
die). This prevents these messages from appearing in terminal. 

### Aliases {#Useful.bash_profilesettings-Aliases .p1}

Aliases are useful for shortening commands that you often use during
your terminal session. You can think of it like creating a variable that
holds the command you want to run. Calling the variable runs the
command. Here is a list of useful aliases that you can add to your
.*bash_profile* file. 

> `alias DIR="cd /path/to/directory"` \# Change directly to directory
>
> `alias ll="ls -alh"` \# List all files in list format with human
> readable size
>
> `alias mkdir="mkdir -pv"` \# Default create directory with parent
> directories. Verbose to see directory structure.
>
> `alias ..="cd .."` \# Move back one directory. Because sometime typing
>  `cd ..`  is just too long.

As an example, the first alias above allows you to immediately change to
a chosen directory. This is useful if you repeatedly navigate to a
folder and do not want to type the full path every time. On hpcnode1 I
frequently work out of my project directory. The screenshot below shows
that I\'ve created an alias
as `SEC="cd /scratch/research/projects/trifolium/SEC_Simulation.Evolutionary.Clines/`.
Typing `SEC` from any directory immediately brings me to my project
folder. Notice that there are no spaces around the `=` and that the
command is in quotes.

### Functions {#Useful.bash_profilesettings-Functions}

Functions work the same way in bash as many other scripting language.
They enable you to perform some repeated task as many times as desired.
You can pass arguments to functions and use these to accomplish
different things or perform tasks on those arguments. If you are unsure
how functions in bash work, there is a brief introduction
[here](http://ryanstutorials.net/bash-scripting-tutorial/bash-functions.php){.external-link
rel="nofollow"}. Below is a list of useful functions (*Code blocks were
entered as markdown and then quoted*).

>     # Make directory and immediately move into it
>     mcd () {
>         mkdir -pv $1
>         cd $1
>     }
>
> \
>
>     # Takes zipped file and extracts it. Accepts 
>     # a range of different formats
>     function extract {
>      if [ -z "$1" ]; then
>         # display usage if no parameters given
>         echo "Usage: extract <path/file_name>.<zip|rar|bz2|gz|tar|tbz2|tgz|Z|7z|xz|ex|tar.bz2|tar.gz|tar.xz>"
>      else
>         if [ -f $1 ] ; then
>             # NAME=${1%.*}
>             # mkdir $NAME && cd $NAME
>             case $1 in
>               *.tar.bz2)   tar xvjf ../$1    ;;
>               *.tar.gz)    tar xvzf ../$1    ;;
>               *.tar.xz)    tar xvJf ../$1    ;;
>               *.lzma)      unlzma ../$1      ;;
>               *.bz2)       bunzip2 ../$1     ;;
>               *.rar)       unrar x -ad ../$1 ;;
>               *.gz)        gunzip ../$1      ;;
>               *.tar)       tar xvf ../$1     ;;
>               *.tbz2)      tar xvjf ../$1    ;;
>               *.tgz)       tar xvzf ../$1    ;;
>               *.zip)       unzip ../$1       ;;
>               *.Z)         uncompress ../$1  ;;
>               *.7z)        7z x ../$1        ;;
>               *.xz)        unxz ../$1        ;;
>               *.exe)       cabextract ../$1  ;;
>               *)           echo "extract: '$1' - unknown archive method" ;;
>             esac
>         else
>             echo "$1 - file does not exist"
>         fi
>     fi
>     }

\
:::

::: {.pageSection .group}
::: pageSectionHeader
## Attachments: {#attachments .pageSectionTitle}
:::

::: {.greybox align="left"}
![](images/icons/bullet_blue.gif){height="8" width="8"}
[Document2.pdf](attachments/11436107/11436103.pdf) (application/pdf)\
![](images/icons/bullet_blue.gif){height="8" width="8"} [Screen Shot
2017-04-28 at 11.15.20 PM.png](attachments/11436107/11436106.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"} [Screen Shot
2017-04-28 at 11.15.20 PM.png](attachments/11436107/11436104.png)
(image/png)\
:::
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
