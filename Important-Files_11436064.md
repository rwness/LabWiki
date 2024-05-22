---
title: "TheNessLab : Important Files"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [HPCnode 1 Documentation](HPCnode-1-Documentation_11436057.html)
:::

# [ TheNessLab : Important Files ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Robert Ness]{.author}, last modified on Jul 17, 2018
:::

::: {#main-content .wiki-content .group}
# Chlamydomonas {#ImportantFiles-Chlamydomonas}

## Reference Genome {#ImportantFiles-ReferenceGenome}

------------------------------------------------------------------------

For reference-based analyses in *Chlamydomonas reinhardtii* we use the
version 5.3 genome from Phytozome. It was created by JGI. The reference
did not originally include the plastid or mitochondrial genomes. It
would be problematic to align sequence reads to the genome without these
organelle genomes because the organelle-derived reads may erroneously
align to the nuclear genome. Similarly, the reference genome is based on
strain CC-503 which happens to be a mating type plus strain. That means
when we map MT- strains to the reference their MT- specific genes will
not be mapped. To avoid this I have added the organelle genomes and the
MT- allele. 

### FASTA sequence: {#ImportantFiles-FASTAsequence:}

This is the actual sequence in fasta format. The chromosomes 1 to 17 are
labelled \"chromosome_1, chromosome_2\...chromosome_17\". The organelles
are named cpDNA and mtDNA for chloroplast and mitchondrial genomes
respectively. The mtMinus locus excluding the rest of chromosome 6 is
called mtMinus.

> `/scratch/research/references/chlamydomonas/5.3_chlamy_w_organelles_mt_minus/chlamy.5.3.w_organelles_mtMinus.fasta`

### GFF {#ImportantFiles-GFF}

If you want to know where the genes are the annotation of all genes
including those in the organelles and MT- are found here:

> `/scratch/research/references/chlamydomonas/5.3_chlamy_w_organelles_mt_minus/annotation/concatenated_GFF/final.strict.GFF3`

[Annotation table]{style="font-size: 16.0px;font-weight: bold;"}

I have also created a large table which documents many genomic features
of the Chlamydomonas reference genome where each site in the reference
genome is represented by a line of the file. It\'s pretty much a big
table. The columns of the table are documented in the header of the file
with lines that start with \##

> `/scratch/research/references/chlamydomonas/5.3_chlamy_w_organelles_mt_minus/annotation/concatenated_GFF/annotation_table.txt.gz`

## Alignments (BAMs) {#ImportantFiles-Alignments(BAMs)}

------------------------------------------------------------------------

### Quebec {#ImportantFiles-Quebec}

Quebec is the only area where there are many samples from a single
geographic area. There are two samples, 4 that start with CC-293\[5678\]
and 20 that start with CC-30\[5678\]\[0-9\]

All the quebec samples from the set of natural strains that start with
CC-30

> `/scratch/research/data/chlamydomonas/quebec/Individual.InDelRealigned.BAMs`

The combined bam of CC-30's is here

> `/scratch/research/data/chlamydomonas/quebec/BAMs/quebec_wt.realigned.bam`

### Species-Wide {#ImportantFiles-Species-Wide}

I refer to all natural strains excluding CC-30's as the species-wide
sample. This is in reference to the fact that these samples range from
Florida, to Minnesota to Quebec. 

Notes- there is reason to believe that CC-2932 has been contaminated
with another algal species (personal communication with Rory Craig) - we
can instead use the Jang et al version of that strain (see below)

**Individual BAMs**

> `/scratch/research/data/chlamydomonas/species_wide/Individual.InDelRealigned.BAMs`

**Combined BAM**

> `/scratch/research/data/chlamydomonas/species_wide/BAMs/species_wide.realigned.bam`

**Jang and Ehrenreich Sequence**

**in Jang H, Ehrenreich IM (2012) Genome-Wide Characterization of
Genetic Variation in the Unicellular, Green Alga Chlamydomonas
reinhardtii. PLoS ONE 7(7): e41307.
[https://doi.org/10.1371/journal.pone.0041307](https://doi.org/10.1371/journal.pone.0041307){.external-link
rel="nofollow"} the authors sequences a bunch of the same wildtype C.
reinhardtii. I\'ve downloaded those onto HPCNODE1 here and they can be
used especially because they have longer reads.\
**

> `/scratch/research/data/chlamydomonas/species_wide/Individual.InDelRealigned.BAMs`

### Mutation Accumulation {#ImportantFiles-MutationAccumulation}

Within this folder there are combined BAMs for each of the 6 ancestral
strains There is also one folder for each of the 6 ancestral lines where
each of the MA lines has an independent BAM

> `/scratch/research/data/chlamydomonas/bgi_full_MA/realigned_bams`

## VCFs {#ImportantFiles-VCFs}

------------------------------------------------------------------------

### Quebec {#ImportantFiles-Quebec.1}

`all_quebec` VCF has ALL 24 Quebec strains - 4 x `CC293[5678]` and 20 x
`CC30[5678][0-9]`

> `/scratch/research/data/chlamydomonas/quebec/VCFs/all_quebec.HC.vcf.gz`

The `quebec` one is only the 20 x `CC-30[5678][0-9]`

> `/scratch/research/data/chlamydomonas/quebec/VCFs/quebec.HC.vcf.gz`

### Species-Wide {#ImportantFiles-Species-Wide.1}

The species wide VCF includes all wild strains excluding the CC30\'s
This VCF was called using HaplotypeCaller in haploid mode:

> `/scratch/research/data/chlamydomonas/species_wide/VCFs/species_wide.HC.vcf.gz`

This one is called using the older UnifiedGenotyper in diploid mode.

> `/scratch/research/data/chlamydomonas/species_wide/VCFs/species_wide.UG_2N.vcf.gz`

## VCFs {#ImportantFiles-VCFs.1}

------------------------------------------------------------------------

### Quebec  CC-30\'s {#ImportantFiles-QuebecCC-30's}

The 20 `quebec` `CC-30[5678][0-9] strains are here:`

/scratch/research/data/chlamydomonas/quebec/fastq/CC3068_wt.2.fq.gz

-   additional Quebec strains CC-29\"s are found in species wide\...

\

\

[Species-Wide]{style="font-size: 16.0px;font-weight: bold;"}

Each of the species-wide strains are found in their own folder here:

`/scratch/research/data/chlamydomonas/species_wide/fastq/`\

These samples were given to us by collaborators from NYU - they have
slightly different names - starting with CR but the numbers  (eg
CR-2344) are equivalent.

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
