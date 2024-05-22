---
title: "TheNessLab : File Structure of HPCnode1"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [HPCnode 1 Documentation](HPCnode-1-Documentation_11436057.html)
:::

# [ TheNessLab : File Structure of HPCnode1 ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Robert Ness]{.author}, last modified on Apr 26, 2017
:::

::: {#main-content .wiki-content .group}
## Your Home folder {#FileStructureofHPCnode1-YourHomefolder}

------------------------------------------------------------------------

In linux your home or user folder will always be here:

> /home/your_utorid

When you login to the server using ssh, or ftp this is the default
folder you will be in. This folder is private and not accessible by
other users. It's a good place to hide your mess

### Don't store large datafiles in your home folder {#FileStructureofHPCnode1-Don’tstorelargedatafilesinyourhomefolder}

By design the `/home/utorid/` folders have a very limited storage
capacity. It is generally meant for small summaries, your scripts etc.
If you try to generate large files in this folder you will fill the
whole thing and no one will be able to work.

\

## Research folder {#FileStructureofHPCnode1-Researchfolder}

------------------------------------------------------------------------

All the research data and projects are stored in a folder called
`research` which is temporarily stored in `/scratch/`

> /scratch/research/

The fact that the research folder is in scratch is a historical
idiosyncrasy of hpcnode1. In the future research will be move one level
up to the root. The `/scratch` folder on our server will not be emptied
regularly like the scratch on other systems

\

## Data folder {#FileStructureofHPCnode1-Datafolder}

------------------------------------------------------------------------

All core data to be shared by multiple projects should be stored in:

> research/data/

Files in this folder can not be moved or deleted, nor can most users
create new files within research/data. This arrangement is not to make
your life difficult but to protect the data against stupidity. Within
research/data/ datasets are organized broadly by taxonomy (e.g.
`chlamydomonas`) and then by dataset (e.g. `bgi_full_MA`).

## Projects folder {#FileStructureofHPCnode1-Projectsfolder}

------------------------------------------------------------------------

The majority of our work is done within a project folder.

> research/projects

Like the data folder, the project folder is first divided by taxonomy or
theme. This allows some hierarchical organization of projects. A project
is a good unit of organization and should roughly correspond to a
publication. Only administrators can create new project folders but the
project leader and other members should be able to alter files within
each project folder.

### Structure within projects {#FileStructureofHPCnode1-Structurewithinprojects}

Within project organization is up to the project leader. In general it
is recommended to make `/analysis`{style="font-size: 14.0px;"} and
`analysis/subanalysis`{style="font-size: 14.0px;"} folders for each
unique component of a project. Each folder should contain documentation
explaining the files within that analysis and how they were created. If
data from the `research/data`{style="font-size: 14.0px;"} file are used
I think its a good idea to use "symbolic links" from the original data
file to a data folder within the project. e.g.

    ln -s /scratch/research/data/chlamydomonas/quebec/VCFs/all_quebec.HC.vcf.gz/scratch/research/data/chlamydomonas/all_quebec.HC.vcf.gz /scratch/research/projects/chlamydomonas/my_project/data/

Using links like this serves three purposes.

1.  First it means that the project should be self contained and not
    require data or code from outside the project.
2.  Links avoid duplicating huge files and clogging up our server.
3.  This ensures that everyone is using the same core data files and
    improves consistency, and reproducibility of research

## Repos folder {#FileStructureofHPCnode1-Reposfolder}

------------------------------------------------------------------------

repos is short for repositories - this folder

> research/repos

holds communal computer code that can and should be shared across many
projects and analyses. Each repo is version controlled by GIT. Members
of the lab are encouraged to take part in developing each repo as
necessary. Please talk to PI Rob Ness if you would like to alter an
existing repo or create a new one.

## Reference genome folder {#FileStructureofHPCnode1-Referencegenomefolder}

------------------------------------------------------------------------

Much of the research in the Ness lab uses reference genome sequences. It
is especially important for reference-based genome assembly. To ensure
that everyone is working from the same reference genomes and to avoid
clashes between corrupt files or changing versions of reference genomes
all reference genomes are stored in:

> research/references

References are grouped taxonomically much like projects and data

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
