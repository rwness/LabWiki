---
title: "TheNessLab : Getting started with Conda on HPCnode1"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [HPCnode 1 Documentation](HPCnode-1-Documentation_11436057.html)
:::

# [ TheNessLab : Getting started with Conda on HPCnode1 ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ James Santangelo]{.author}, last modified by [ Ahmed Raza
Hasan]{.editor} on Apr 13, 2021
:::

::: {#main-content .wiki-content .group}
# Rationale for software installs on HPCnode1 {#GettingstartedwithCondaonHPCnode1-RationaleforsoftwareinstallsonHPCnode1}

We\'ve adopted a software installation strategy on HPCnode1 that
minimizes the number of software packages and utilities that are
globally installed on the system. Common utilities (e.g., Vim, Git,
etc.) are installed globally, but other installs should be installed on
project-by-project basis into isolated environments using Conda.
However, the (base) Conda environment will additionally contain updated
versions of software packages that are frequently used in the lab\'s
computational work (e.g., samtools, bwa, etc.)

# Using Conda on HPCnode1 {#GettingstartedwithCondaonHPCnode1-UsingCondaonHPCnode1}

Conda is currently globally installed in /opt/anaconda3. When logging on
to HPCnode for the first time, follow the following steps. 

## Getting started with Conda {#GettingstartedwithCondaonHPCnode1-GettingstartedwithConda}

### Initialize Conda {#GettingstartedwithCondaonHPCnode1-InitializeConda}

When using Conda for the first time on HPCnode1, we need to initialize
Conda so it can be used in our everyday work. This can be done by
running `conda init bash` at the command line, which initializes Conda
with Bash as its executing shell. This will automatically append the
following lines to your `.bashrc` file

> [    \# \>\>\> conda initialize \>\>\>]{.s1}
>
> [    \# !! Contents within this block are managed by \'conda init\'
> !!]{.s1}
>
> [    \_\_conda_setup=\"\$(\'/opt/anaconda3/bin/conda\' \'shell.bash\'
> \'hook\' 2\> /dev/null)\"]{.s1}
>
> [    if \[ \$? -eq 0 \]; then]{.s1}
>
> [        eval \"\$\_\_conda_setup\"]{.s1}
>
> [    else]{.s1}
>
> [        if \[ -f \"/opt/anaconda3/etc/profile.d/conda.sh\" \];
> then]{.s1}
>
> [            . \"/opt/anaconda3/etc/profile.d/conda.sh\"]{.s1}
>
> [        else]{.s1}
>
> [            export PATH=\"/opt/anaconda3/bin:\$PATH\"]{.s1}
>
> [        fi]{.s1}
>
> [    fi]{.s1}
>
> [    unset \_\_conda_setup]{.s1}
>
> [    \# \<\<\< conda initialize \<\<\<]{.s1}

Now, when we login to HPCnode1, we will be able to create, activate, and
use conda environments on HPCnode1. If you want to make Conda available
in your current shell instance, you can run `source ~/.bashrc` at the
command line to restart your shell. Your should notice that your shell
prompt has changed and should look something like:

> (base) \<bash_prompt\>

Where `<bash_prompt>` is probably something containing your username on
HPCnode1. What\'s more important is `(base)`, which tells us we are
currently in the `(base)` conda environment. This is the global Conda
environment into which frequently used software packages and utilities
will be installed. 

## Using Conda in everyday work {#GettingstartedwithCondaonHPCnode1-UsingCondaineverydaywork .p1}

The base environment has up-to-date versions of Python and all of the
commonly used numerical data analysis Python modules (e.g., `Pandas`,
`numpy`, `scikit-learn`, `Jupyter`, etc. ). As such, it\'s great if you
just quickly want to spin up an analysis but probably shouldn\'t be used
for dedicated projects for two reasons:

1.  Each project is likely to contain many dependencies, which over
    time, would clutter up the base environment if everyone was
    installing packages in there as part of their workflow
2.  Software installed in the base environment is likely to be
    continuously updated as new version are release, making it harder to
    reproduce project analyses that rely on a specific software
    version. 

For these reasons, you\'ll likely want to create separate environments
for different project so that each project\'s software dependencies are
self-contained. Conda makes this pretty easy, so we\'ll go through an
example here. 

# Creating a new  environment {#GettingstartedwithCondaonHPCnode1-Creatinganewenvironment}

Conda makes creating new environments really easy. On HPCnode1, the
exact command used will depend on whether the environment is going to be
shared by multiple people, or used only by you. Let\'s walk through each
of these.

## Creating shared environments {#GettingstartedwithCondaonHPCnode1-Creatingsharedenvironments}

By default, new Conda environments created on HPCnode1 will be installed
in `/opt/anaconda3/envs`. Because we all have read/write access to this
directory, it\'s the perfect location to installed shared environments
that can be used by any lab member (though there are other ways, as
we\'ll see). 

To create a Conda environment, run the following command at the
command-line:

`conda create --name test`

You should receive a prompt like the one below showing that this
environment will be created in the default location. 

[![](attachments/50758860/50758867.png){.confluence-embedded-image
draggable="false" height="157"
image-src="attachments/50758860/50758867.png"
unresolved-comment-count="0" linked-resource-id="50758867"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_10-59-12.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

Answer \"yes\" to the prompt, and the following will appear describing
how the environment can be activated, we\'ll get to environment
activation shortly. 

[![](attachments/50758860/50758868.png){.confluence-embedded-image
draggable="false" height="191"
image-src="attachments/50758860/50758868.png"
unresolved-comment-count="0" linked-resource-id="50758868"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-1-13.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

That\'s it! We\'ve created a bare Conda environment named \"test\".
It\'s bare because it contains no packages. To install packages, we have
to activate the environment and then install packages into it, which
we\'ll see shortly.

## Creating personal environments {#GettingstartedwithCondaonHPCnode1-Creatingpersonalenvironments}

If you\'re the only one using a Conda environment, it doesn\'t make
sense to install it to the global environment directory. Conda knows
this and has created a hidden folder in your home directory into which
Conda environments can be installed. Here is a screenshot of my home
folder. Notice the `.conda` directory. This is where we should tell
Conda to install personal environments. 

[![](attachments/50758860/50758869.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/50758860/50758869.png"
unresolved-comment-count="0" linked-resource-id="50758869"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-7-1.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

Creating an environment in this directory is very similar to creating
shared environments, but we have to explicitly tell Conda where to
install the environment using the `--prefix` argument. Let\'s see what
this looks like. Let\'s create a personal environment called
\"personal\"

`conda create --prefix ~/.conda/envs/personal`

As we can see, the prompt is largely the same, though the install
location has changed. 

[![](attachments/50758860/50758870.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/50758860/50758870.png"
unresolved-comment-count="0" linked-resource-id="50758870"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-11-19.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

Now that we\'ve installed a few environments, let\'s have a look at all
of the Conda environments installed on the system:

`conda info --envs`

[![](attachments/50758860/50758871.png){.confluence-embedded-image
draggable="false" height="105"
image-src="attachments/50758860/50758871.png"
unresolved-comment-count="0" linked-resource-id="50758871"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-13-45.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

As you can see, we\'ve got the \"base\" environment at `/opt/anaconda3`
and the \"test\" environment we created in the global environment
directory. I\'ve also got two personal environments (\"default\" and
\"personal\") in my home folder\'s Conda environment directory. 

On the left of the image, you can also see the Conda environment\'s
name, which we can use to activate it. Only environments installed into
the global Conda install directory or your home folder can be activated
by name. This is because these are the two locations that Conda
automatically searches for environments during activation. While we can
configure the Conda environment search paths, it likely isn\'t necessary
for our purposes. 

## Create environments in non-standard locations {#GettingstartedwithCondaonHPCnode1-Createenvironmentsinnon-standardlocations}

If you want to create an environment in a difference location (i.e., not
in` /opt/anaconda3/envs` or `~/.conda/envs`), then you can you it the
same way we created the personal environment (using `--prefix`) but
changing the install path. For example, to create an environment in
`/research`, you would do something like:

`conda create --prefix /research/my-env`

Note that activation of this environment will differ slightly from
activation of environments installed in one of the standard locations,
as we\'ll now see. 

## Updating your `envs_dirs` {#GettingstartedwithCondaonHPCnode1-Updatingyourenvs_dirs}

You might notice any envs named with `--prefix` are \'unnamed\' when you
run `conda env list`, looking something like this:

    # conda environment
    #
                /home/username/.conda/env/my_env
                /home/username/.conda/env/other_env
    base        /opt/anaconda3
    briantest   /opt/anaconda3/envs/briantest

To fix this, you have to add the *directory containing your custom envs*
to the `envs_dirs` variable, like so:

`conda config --append envs_dirs /home/username/.conda/env`

This will automatically update their names:

    # conda environment
    #
    my_env      /home/username/.conda/env/my_env
    other_env   /home/username/.conda/env/other_env
    base        /opt/anaconda3
    briantest   /opt/anaconda3/envs/briantest

which also means you can now type `conda activate my_env` as opposed to
the full path every time.

**This is very important to do if you\'re going to be using Jupyter** -
not having \'named\' envs can mess with Jupyter functionality (see
below) for some reason. Be warned!

# Activating an environment {#GettingstartedwithCondaonHPCnode1-Activatinganenvironment}

## Environments in standard install locations {#GettingstartedwithCondaonHPCnode1-Environmentsinstandardinstalllocations}

For environments installed into either `/opt/anaconda3/envs` or
`~/.conda/envs`, we can activate them by name. For example, to activate
the \"personal\" environment we previously created, we would run:

`conda activate personal`

[![](attachments/50758860/50758872.png){.confluence-embedded-image
draggable="false" height="38"
image-src="attachments/50758860/50758872.png"
unresolved-comment-count="0" linked-resource-id="50758872"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-28-20.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

Notice the shell prompt has changed from (base) to (personal). Note that
under the hood, Conda has deactivated (base) before activating
(personal), meaning that none of the software installed in \"base\" will
be available in \"personal\" unless it is also installed there. If you
would like the software installs from \"base\" to remain available, you
can stack your conda environments by running:

`conda activate --stack personal`

This will make all software installed in \"base\" available in
\"personal\", in addition to whatever software is installed in
\"personal\". In cases where the same software is installed in both
environments, the environment on top of the stack takes precedence
(\"personal\" in this case)

## Environments in non-standard locations {#GettingstartedwithCondaonHPCnode1-Environmentsinnon-standardlocations}

For environments installed to non-standard locations, we have to
activate them using the full path to the environment. As an example,
let\'s first create an environment in a non-standard location

`conda create --prefix /research/projects/trifolium/test`

We can now activate this environment by specifying its full path 

`conda activate /research/projects/trifolium/test`

As you can see below, the environment is activated. The only downside to
this approach is that it can result in really long shell prompt since
the Conda environment\'s name is now its full path, though this can be
configured in Conda\'s configuration file (the `~/.condarc` file, see
[HERE](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html){.external-link
rel="nofollow"}) 

[![](attachments/50758860/50758873.png){.confluence-embedded-image
draggable="false" height="39"
image-src="attachments/50758860/50758873.png"
unresolved-comment-count="0" linked-resource-id="50758873"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_11-38-56.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

\

In short if you enter this command conda will use the root name instead
of the full path:

    conda config --set env_prompt '({name})'

We\'re now ready to start installing packages. 

# Installing packages {#GettingstartedwithCondaonHPCnode1-Installingpackages}

Regardless of environment or software package, install software via
Conda require knowledge of 3 things:

1.  The Conda channels: This is basically the online repositories where
    Conda will search for the requested packages. Many packages can be
    found in multiple channels, so making sure you get the right one is
    essential. Thankfully, there are only a handful of
    community-maintained repositories you\'re likely to need so this is
    quite simple. 
2.  The software package name
3.  (optional) The software package\'s version. If the version is not
    specified, Conda will install the latest version by default. 

A typical command to install a piece of software will look something
like:

`conda install -c <channel> <package> `

For example let\'s install `samtools` into our \"personal\" Conda
environment, which is available via the `bioconda` channel

`conda install -c bioconda samtools`

You\'ll get something that looks like the image below showing all of the
packages that will be installed. 

[![](attachments/50758860/50758874.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/50758860/50758874.png"
unresolved-comment-count="0" linked-resource-id="50758874"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_12-3-42.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

We now have the latest version of samtools installed. Now let\'s say we
also specifically need version 3.8.6 of Python. We can install this in
the same way but specifying the version of Python

`conda install -c anaconda Python=3.8.6`

Notice the \"=\" sign after the package name specifying the version.
This syntax works for all software. Finally, you can install multiple
software package simultaneously, even if they\'re in different
channels. 

[`conda install -c conda-forge -c anaconda r-base=3.6.3 Python=3.8.6`]{style="color: rgb(51,51,51);"}

[This command would install version 3.6.3 of R and v. 3.8.6 of
Python. ]{style="color: rgb(51,51,51);"}

[After installing packages, it\'s good practice to run
`conda clean --all` and answer \"y\" to all of the prompts. This will
get rid of extraneous caches and tarballs associated with package
installs that just take up space for no good
reason.]{style="color: rgb(51,51,51);"}

[If you\'re unsure which channel a package is in, the easiest thing to
do is to search for \"conda \<package name\>\" on Google. The first hit
will almost always be what you\'re looking for and should point to
Anaconda.org. Here are some common channel\'s you\'re likely to
encounter:]{style="color: rgb(51,51,51);"}

-   [conda-forge]{style="color: rgb(51,51,51);"}
-   [anaconda]{style="color: rgb(51,51,51);"}
-   [bioconda]{style="color: rgb(51,51,51);"}
-   [r]{style="color: rgb(51,51,51);"}

[Because some software are maintained in multiple channels, it\'s better
to be explicit about which channels to search when installing packages
via the command line rather than setting globally configured channels to
search. For example, R is available through both the \"r\" channel and
through \"conda-forge\", the latter of which is more heavily maintained
and stable. ]{style="color: rgb(51,51,51);"}

If you follow these steps, you should be able to install any software
that is available through Conda, whether it be an R package, Python
package, or independent piece of software. 

## Updating and removing packages {#GettingstartedwithCondaonHPCnode1-Updatingandremovingpackages}

Packages can be easily update by running 

conda update \<package-name\>

Similarly, they can be remove by running 

conda remove \<package-name\>

## Adding your Conda environment to Jupyter {#GettingstartedwithCondaonHPCnode1-AddingyourCondaenvironmenttoJupyter}

You\'d think that starting a Jupyter instance after activating an
environment would allow you to access the packages installed in that
environment, but if that doesn\'t work, you likely have to set up the
environment separately as an option in the Jupyter launcher.

First, in my experience, **this method doesn\'t work with `--prefix`
environments unless they\'ve been added to** **`envs_dirs`** (see above)
like so:

`conda config --append envs_dirs ~/.conda/env`

where `~/.conda/env` contained the environments you want to use. It is
important *not* to write the path to the environment itself here.

Once you\'ve done this, install `nb_conda_kernels` like so:

`conda install nb_conda_kernels`

and you should see new option(s) in your Launcher with your custom
environments.

If this is still failing, try running

`python -m ipykernel install --user --name [env] --display-name "desired env name"`

to force the addition of the env to Jupyter.

# Tips and tricks {#GettingstartedwithCondaonHPCnode1-Tipsandtricks}

## Listing packages {#GettingstartedwithCondaonHPCnode1-Listingpackages}

Sometimes it\'s useful to have a list of packages installed in the
current environment. You can get this by running:

`conda list`

## Exporting environment {#GettingstartedwithCondaonHPCnode1-Exportingenvironment}

Instead of listing the packages, you might want to export them to a
file, which would allow you and others to create identical environments
on another machine. You can do this by running:

`conda env export > environment.yaml`

Running this on our \"personal\" environment yields a file that looks
like this, containing only `samtools` and related dependencies. 

[![](attachments/50758860/50758877.png){.confluence-embedded-image
draggable="false" height="400"
image-src="attachments/50758860/50758877.png"
unresolved-comment-count="0" linked-resource-id="50758877"
linked-resource-version="1" linked-resource-type="attachment"
linked-resource-default-alias="image2021-2-24_12-24-53.png"
base-url="https://wiki.utm.utoronto.ca"
linked-resource-content-type="image/png"
linked-resource-container-id="50758860"
linked-resource-container-version="14"}]{.confluence-embedded-file-wrapper
.confluence-embedded-manual-size}

## Creating an environment from a file {#GettingstartedwithCondaonHPCnode1-Creatinganenvironmentfromafile}

To create a new Conda environment from a file like the one above, we can
run something like:

`conda env create --file environment.yaml --name test`

Notice the use of Conda env create rather than Conda create. This syntax
is used specifically to create an environment from a file. 

You can use `--prefix` instead of `--name` to install this environment
in a location other than `/opt/anaconda3/envs`

# When Conda isn\'t enough {#GettingstartedwithCondaonHPCnode1-WhenCondaisn'tenough}

The list of software available through Conda is extensive and always
growing, but it doesn\'t have everything. For example, you might be
using some obscure R package or piece of software that hasn\'t been
ported to Conda. The solution to this depends on the particular use
case. 

## Python packages not available through Conda {#GettingstartedwithCondaonHPCnode1-PythonpackagesnotavailablethroughConda}

This is quite easy. If a package isn\'t available through Conda, you can
install it using pip the same way you would a regular Python package.
Doing so will still install the package into your current environment. 

`pip install <package>`

\

If, however, your package isn\'t available on pip (e.g. a custom set of
scripts, such as the ness_vcf and vcf2fasta utilities we have on the
server), getting conda to recognize these can get a little hairy. One
way - perhaps not the optimal way, but one that works - is to symlink
the scripts into your `site-packages` directory. Once your environment
has been activated, start a Python instance by simply typing `python`
(or whichever specific version you care about, e.g. `python3.6`) and run

\

``` python
import site
site.getsitepackages()
```

\

The `getsitepackages()` function will return your `site-packages`
directory path - this will look something like
`~/.conda/env/envname/lib/python3.6/site-packages`.

\

Head to this directory in bash and symlink the scripts you want in here.
For example:

\

``` bash
ln -s /research/repos/ness_vcf/ness_vcf.py .
```

\

This will create a shortcut to the `ness_vcf` script in `site-packages`,
and your instance of Python will now be able to access those custom
functions/classes. Once again - ugly, sure, but it\'s worked so far.

\

## R packages not available through Conda {#GettingstartedwithCondaonHPCnode1-RpackagesnotavailablethroughConda}

This is a little trickier since Conda is primarily built around Python
and doesn\'t have native support for R. However, we can install R
dependency management packages through Conda and use those to install R
packages through CRAN or Github. In my view, the current gold-standard
for managing R packages is the `renv` package, available through the
conda-forge channel

[`conda install -c conda-forge r-renv`]{style="color: rgb(51,51,51);"}

[I won\'t go into how to use renv here, but there are some great
tutorials online, including [this
one](https://rstudio.github.io/renv/articles/renv.html){.external-link
rel="nofollow"}. ]{style="color: rgb(51,51,51);"}

An advantage of `renv` is that it also allows installation of R packages
that are available through Github in addition to CRAN. 

## When all else fails {#GettingstartedwithCondaonHPCnode1-Whenallelsefails}

For everything else, Code can be run inside of isolated
Singularity/Docker containers. Because these start out as bare linux
kernels, you can install any required software dependencies and don\'t
have to rely on externally managed repositories. You can simply get the
software you need, install it in the container, and run all of your code
inside the container using Singularity, which is now installed on
HPCnode1. In theory, you could have a single container per project,
containing all of the required software dependencies, but the learning
curve to creating such a container might be a little steep, which is why
this should be a last resort and why Conda is so great. 

Nonetheless, here is an example of such a container for NGSLD, a
software package for estimating LD from low-coverage genomic data. This
package is not available through Conda or any other repository. After
the container is created, it can easily be used to execute script and
code on HPCnode1 with only a few commands

INSERT COMMANDS OR LINK TO TUTORIAL

If you\'re convinced you can\'t get the software any other way, this
might be your best bet. Your first container might take you a day to
create, but future ones will take less than an hour. Alternatively, you
can bribe someone who knows how to create them and if your offer is
sufficient, they might be willing to help you
out ![(tongue)](images/icons/emoticons/tongue.svg){.emoticon
.emoticon-cheeky emoticon-name="cheeky"}. 

\

## How to solve `NotWritableError`  {#GettingstartedwithCondaonHPCnode1-HowtosolveNotWritableError}

Some of us get a NotWritableError  when trying to create environments,
etc.

The issue is Conda is storing all of the package caches in
/opt/anaconda3/pkgs/cache/ so if someone else has already installed that
package, the cache will be present. When someone else tries to install
the same package, Conda knows that it's cached, tries to read it from
the global cache, but fails since the new user doesn't have read
permissions on the cache.

The solution is to tell Conda to store pkgs and caches only in your home
directory. You can do this by creating a file \~/.condarc that stores
these config settings:

> `envs_dirs:`\
> `- ~/.conda/envs`\
> `- /opt/anaconda/envs`\
> `pkgs_dirs:`\
> `- ~/.conda/pkgs`

This will explicitly tell Conda that environments might be global or in
HOME but that pkgs will be only in HOME, where everyone has read/write
permissions

\

\

\
:::

::: {.pageSection .group}
::: pageSectionHeader
## Attachments: {#attachments .pageSectionTitle}
:::

::: {.greybox align="left"}
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_10-59-4.png](attachments/50758860/50758866.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_10-59-12.png](attachments/50758860/50758867.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-1-13.png](attachments/50758860/50758868.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-7-1.png](attachments/50758860/50758869.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-11-19.png](attachments/50758860/50758870.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-13-45.png](attachments/50758860/50758871.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-28-20.png](attachments/50758860/50758872.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_11-38-56.png](attachments/50758860/50758873.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_12-3-42.png](attachments/50758860/50758874.png)
(image/png)\
![](images/icons/bullet_blue.gif){height="8" width="8"}
[image2021-2-24_12-24-53.png](attachments/50758860/50758877.png)
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
