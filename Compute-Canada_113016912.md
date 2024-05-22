---
title: "TheNessLab : Compute Canada"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
:::

# [ TheNessLab : Compute Canada ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Jimmy Issa]{.author}, last modified on Sep 25, 2023
:::

::: {#main-content .wiki-content .group}
## [Introduction]{style="color: rgb(0,0,0);"} {#ComputeCanada-Introduction}

[Compute Canada is a national infrastructure developed by the Digital
Research Alliance of Canada to enhance the ability of Canadian
researchers to perform work that requires much compute power. This
represents an alternative to HCPnode1 and UTM High Performance
Computing.]{style="color: rgb(0,0,0);"}

[The two main websites are:]{style="color: rgb(0,0,0);"}

-   [[https://ccdb.alliancecan.ca/](https://ccdb.alliancecan.ca/){.external-link
    style="color: rgb(0,0,0);" rel="nofollow"} (main site for creating
    and renewing your account, requesting a role in your supervisors
    allocation for non-faculty resources,
    etc)]{style="color: rgb(0,0,0);"}
-   [[https://docs.alliancecan.ca/wiki/Technical_documentation](https://docs.alliancecan.ca/wiki/Technical_documentation){.external-link
    style="color: rgb(0,0,0);" rel="nofollow"} (all the technical
    documentation for using Compute Canada)]{style="color: rgb(0,0,0);"}

[Everything you need to know has already been answered in the technical
documentation. ]{style="color: rgb(0,0,0);"}

## [Creating an account]{style="color: rgb(0,0,0);"} {#ComputeCanada-Creatinganaccount}

[Begin by just creating an account using your university email on the
main website. You need to request your supervisor to give you access to
their allocation (i.e. their share of computing resources granted to
them by Compute Canada). This is called creating a \"role\", and the
account which has the allocation that you are given access to is called
the \"sponsor\". To do this, the sponsor must give you a unique
identifier to their allocation called a CCRI key which you will use when
requesting a role on the main website. The sponsor will have to approve
this on their end, and when they do, it will allow you to directly
request access to their allocation. Once this is done, you should be
able to see the status of your role on the main website as \'activated\'
(or alternatively, \'recently activated\'). Once you see this, you
should be able to remotely access the allocation.
]{style="color: rgb(0,0,0);"}

## [Accessing Compute Canada]{style="color: rgb(0,0,0);"} {#ComputeCanada-AccessingComputeCanada}

[To actually access this resource, you will need to ssh via a Linux
system, such as a Bash or Zsh terminal. If you do not know what ssh is
or what Linux is, you need to figure that out first before
proceeding.]{style="color: rgb(0,0,0);"}

[To connect to the allocation, open your terminal and type
this:]{style="color: rgb(0,0,0);"}

[ssh username@cluster.computecanada.ca]{style="color: rgb(0,0,0);"}

[You will need to replace two things in this line: replace \'username\'
with your username on the main Compute Canada website (see top of this
page), and \'cluster\' with one of the five main clusters made available
by Compute Canada. The options are Cedar, Graham, Narval, Beluga, and
Niagara. For example, if your username is \"jimmy_issa\" and you want to
use Cedar, you would do:]{style="color: rgb(0,0,0);"}

[ssh jimmy_issa@cedar.computecanada.ca]{style="color: rgb(0,0,0);"}

[This should remotely connect you to to the allocation, although you
will be prompted to enter your password. This is the same password you
would use to log into the main Compute Canada website. I recommend
setting up an SSH key so that you are not prompted for a password every
time you log in (and this is also more secure). See
[here](https://docs.alliancecan.ca/wiki/SSH_Keys){.external-link
rel="nofollow"} for details on how to add an SSH
key.]{style="color: rgb(0,0,0);"}

## [Special Compute Canada commands]{style="color: rgb(0,0,0);"} {#ComputeCanada-SpecialComputeCanadacommands}

[sbatch (to submit a job)]{style="color: rgb(0,0,0);"}

[salloc (for submitting interactive jobs, eg a Jupyter
session)]{style="color: rgb(0,0,0);"}

[sq (to see all your running jobs)]{style="color: rgb(0,0,0);"}

[squeue (to see all jobs in the queue that the scheduler is
managing)]{style="color: rgb(0,0,0);"}

[scancel \<job-id\> (to cancel a job)]{style="color: rgb(0,0,0);"}

[sacct (to list completed jobs)]{style="color: rgb(0,0,0);"}

[srun (I dont know anything about this one)]{style="color: rgb(0,0,0);"}

[I think that the \'s\' in all these commands stands for \'submit\', but
I\'m not sure. ]{style="color: rgb(0,0,0);"}[Anyways, let\'s say that
you submit using sbatch and you want to know how many other jobs are
ahead of you in the query before your own is processed. You can directly
use the following command to tell you this (replace  \'username\' with
your own username):]{style="color: rgb(0,0,0);"}

[squeue \| nl \| grep username]{style="color: rgb(0,0,0);"}

To check the number of jobs ahead of you:

squeue \| nl \| grep jimmissa

To see your jobs:

sq

squeue -u username

To specify seeing your running or pending jobs:

squeue -u username -t RUNNING

squeue -u username -t PENDING

To show specific information about a job:

scontrol show job -dd \<jobid\>

Here are two ways to cancel all your jobs:

scancel \$(squeue \| grep jimmissa \| awk \'{print \$1}\')

scancel -u\$USER to cancel all your jobs

Note that when you run sbatch, a file called \"slurm-%j.out\" will be
created, where the \"%j\" is replaced with the job id or job allocation
number. It will contain both the stdout and stderr of your script.

## How the script you should submit for running a job should actually look like {#ComputeCanada-Howthescriptyoushouldsubmitforrunningajobshouldactuallylooklike}

[According to the documentation, the following is the simplest Bash
script you can submit to Compute Canada:]{style="color: rgb(0,0,0);"}

    #!/bin/bash
    #SBATCH --time=00:15:00
    #SBATCH --account=def-someuser
    echo 'Hello, world!'
    sleep 30

    The #SBATCH lines in this example specify the expected time the job will take and the username of your supervisor/sponsor, eg def-nessrobe for Rob.
    The following demonstrates other #SBATCH lines you can add:

[#!/bin/bash]{style="color: rgb(0,0,0);"}

[#SBATCH \--account=def-nessrobe]{style="color: rgb(0,0,0);"}

[#SBATCH \--nodes=1]{style="color: rgb(0,0,0);"}

[#SBATCH \--ntasks=16]{style="color: rgb(0,0,0);"}

[#SBATCH \--cpus-per-task=1]{style="color: rgb(0,0,0);"}

[#SBATCH \--mem=80G]{style="color: rgb(0,0,0);"}

[#SBATCH \--time=0-10:00]{style="color: rgb(0,0,0);"}

[It is important to consult the documentation and/or more detailed
tutorials (eg [this
one](https://prashp.gitlab.io/post/compute-canada-tut/){.external-link
rel="nofollow"}) to have a more precise understanding of all this,
though.]{style="color: rgb(0,0,0);"}

## [The Module command]{style="color: rgb(0,0,0);"} {#ComputeCanada-TheModulecommand}

You should also have an understanding of the \'module\' command, which
you use to manage your environment and modify the software available to
it. The module command is used with a range of possible subcommands.
Here are all the ones I know and what they do:

module spider (or module spider \<module-name\>): list available
software packages.

module \--show_hidden spider \<module-name\>: for listing experimental
modules.

module avail: list currently loadable software packages.

module load \<module-name\>: load the default version of a particular
software.

module load \<module-name\>/\<module-version\>: load a specific version
of a particular software.

module list: list loaded modules.

module purge: unload all currently loaded modules.

module show \<module-name\>: shows much more info about a software: 
short description, included extensions, dependencies, and the specific
path as to where it is stored.

Let\'s say you have an ideal combination of loaded modules, such as for
a specific project. You can save your current set of loaded modules
(with a name you specify) into a module set and restore it as follows:

module save MYMODULES

module restore MYMODULES

module savelist: to list all your saved module combinations

module describe MYMODULES: shows you the specific modules saved in a
given module set

The following loads numpy, pandas, scipy, matplotlib, IPython, Sympy,
and nose:

module load scipy-stack

## Jupyter {#ComputeCanada-Jupyter}

There are two ways to access Jupyter via Compute Canada:

1.  The simplest way is to access it from the web:
    [https://jupyterhub.cluster.computecanada.ca/user/username/](https://jupyterhub.cluster.computecanada.ca/user/username/){.external-link
    rel="nofollow"}. Replace \'cluster\' with the desired cluster and
    \'username\' with your username. You will be asked to launch a
    server and specify a couple options when doing so (e.g. the amount
    of memory you want to use, how long you want it to stay open).
2.  Open it as a Slurm job from within Bash. This option is more
    complicated and you need to follow the docs to figure out how to do
    it: see
    [here](https://docs.alliancecan.ca/wiki/JupyterNotebook){.external-link
    rel="nofollow"}.

If you use (2), keep in mind that you will use pip with the \--no-index
flag to install software, i.e. pip install \--no-index package_name. You
can do this from the terminal (so long as you\'re in the right virtual
environment when doing so) or from within a Jupyter cell.

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
