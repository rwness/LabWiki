---
title: "TheNessLab : cyvcf2 tutorial"
---

::: {#page}
::: {#main .aui-page-panel}
::: {#main-header}
::: {#breadcrumb-section}
1.  [TheNessLab](index.html)
2.  [The Ness Lab Wiki](The-Ness-Lab-Wiki_11436042.html)
3.  [Coding tips and tutorials](Coding-tips-and-tutorials_11436186.html)
:::

# [ TheNessLab : cyvcf2 tutorial ]{#title-text} {#title-heading .pagetitle}
:::

::: {#content .view}
::: page-metadata
Created by [ Ahmed Raza Hasan]{.author}, last modified on Dec 26, 2020
:::

::: {#main-content .wiki-content .group}
## Intro {#cyvcf2tutorial-Intro}

If you\'ve been working with VCF files at all, you\'ll know they can be
quite large and unwieldy to work with. Historically, our lab (and
others) have used a Python library called
[pyVCF](https://pyvcf.readthedocs.io/en/latest/){.external-link
rel="nofollow"} to parse VCF files. While it\'s done the job, it\'s
definitely not the fastest or most efficient parser out there.

Enter
[cyvcf2](https://academic.oup.com/bioinformatics/article/2971439/cyvcf2){.external-link
rel="nofollow"}. While this Python library does the same thing pyVCF
does, it does everything *stupidly fast* - a very important advantage
when working with massive datasets.

Below is a quick surface level tutorial on how to use `cyvcf2`,
juxtaposed with equivalent `pyVCF` commands for those who are more
familiar with the latter.

## Getting started {#cyvcf2tutorial-Gettingstarted}

Let\'s import both libraries into our workspace:

    import vcf # pyvcf
    from cyvcf2 import VCF # cyvcf

We\'ll also import a useful package for timing loops:

    from tqdm import tqdm

If any of the above lines raises some sort of \'package not found\'
error, head back to a bash terminal and run this:

    pip install --user cyvcf2
    pip install --user tqdm

## Basic iteration {#cyvcf2tutorial-Basiciteration}

Let\'s start with something simple: how many variants are in a given VCF
file?

I\'m going to be working off a file called `chromosome_15.vcf.gz`. A
bash oneliner tells us this file has 62,000 variants in it:

    zgrep -v '#' chromosome_15.vcf.gz | wc -l # 62701

But we care about how this is done in Python right now. For both
packages, we\'ll have to create a loop to iterate through the records in
the file.

### pyVCF {#cyvcf2tutorial-pyVCF}

Here\'s pyVCF\'s take on iteration. We\'ll time it with `tqdm` by
wrapping the iterable (i.e. the `y` part of `for x in y`) in `tqdm()`.

    fname = 'chromosome_15.vcf.gz'
    counter = 0

    for record in tqdm(vcf.Reader(filename=fname, compressed=True)):
        counter += 1

Here\'s the `tqdm` report:

    62701it [00:20, 3057.36it/s]

### cyvcf2 {#cyvcf2tutorial-cyvcf2}

How does `cyvcf2`\'s iteration look, and how does it fare against that
20 second time?

    fname = 'chromosome_15.vcf.gz'
    counter = 0

    for record in tqdm(VCF(fname)):
        counter += 1

It takes literally less than a second to do this operation:

    62701it [00:00, 87690.59it/s]

cyvcf2 also is good about inferring whether a VCF is bgzipped or not, so
the filename is all that\'s needed as an input argument to `VCF`.

## Fetching a specific region {#cyvcf2tutorial-Fetchingaspecificregion}

cyvcf2 is also just as capable as pyVCF when it comes to fetching
records in specific regions. However, its syntax is a little strange in
that instead of using a specific method, we provide the region as input
to the iterator itself, writing syntax as if the iterator was a function
and not an object.

Let\'s repeat the above operation for `chromosome_15:100000-500000` to
see how many variants we have in that region.

### pyVCF {#cyvcf2tutorial-pyVCF.1}

This time, we\'ll assign the iterator to a second object called `v`.

    fname = 'chromosome_15.vcf.gz'
    counter = 0

    v = vcf.Reader(filename=fname, compressed=True)

    for record in tqdm(v.fetch('chromosome_15', 100000, 500000)):
        counter += 1

### cyvcf2 {#cyvcf2tutorial-cyvcf2.1}

    fname = 'chromosome_15.vcf.gz'
    counter = 0

    v = VCF(fname)

    for record in tqdm(v('chromosome_15:100000-500000')):
        counter += 1

The main takeaway is that cyvcf2 expects a string containing a
tabix-formatted region (`chr:start-end`) written as if the VCF object
itself was a function. This strange syntax is made possible because it
uses the `__call__` method under the hood to interpret the string.
Either way, still takes less than a second to run: blink and you\'ll
miss it.

## Inspecting individual records {#cyvcf2tutorial-Inspectingindividualrecords}

This is another area where the two packages diverge a bit.

### pyVCF {#cyvcf2tutorial-pyVCF.2}

Let\'s pull out the first record from the VCF and look at it:

    v = vcf.Reader(filename=fname, compressed=True)
    rec = next(v)
    print(rec)
    # <vcf.model._Record object at 0x7f806e7670f0>

Here are the methods/attributes available to us:

    >>> dir(rec)
    ['ALT', 'CHROM', 'FILTER', 'FORMAT', 'ID', 'INFO', 'POS', 'QUAL', 'REF', 
    '__class__', '__cmp__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', 
    '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__iter__', 
    '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', 
    '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 
    '_compute_coordinates_for_indel', '_compute_coordinates_for_none_alt', '_compute_coordinates_for_snp', 
    '_compute_coordinates_for_sv', '_sample_indexes', '_set_start_and_end', 'aaf', 'add_filter', 
    'add_format', 'add_info', 'affected_end', 'affected_start', 'alleles', 'call_rate', 'end', 
    'genotype', 'get_hets', 'get_hom_alts', 'get_hom_refs', 'get_unknowns', 'heterozygosity', 
    'is_deletion', 'is_indel', 'is_monomorphic', 'is_snp', 'is_sv', 'is_sv_precise', 'is_transition', 
    'nucl_diversity', 'num_called', 'num_het', 'num_hom_alt', 'num_hom_ref', 'num_unknown', 
    'samples', 'start', 'sv_end', 'var_subtype', 'var_type']

Importantly, pyVCF records contain `Call` subclasses, which store call
info for each included genotype:

    >>> rec.samples
    [Call(sample=CC2935, CallData(GT=0, AD=[1, 0], DP=1, GQ=45, PL=[0, 45])), 
    Call(sample=CC2936, CallData(GT=0, AD=[6, 0], DP=6, GQ=99, PL=[0, 221])), 
    Call(sample=CC2937, CallData(GT=0, AD=[2, 0], DP=2, GQ=45, PL=[0, 45])), 
    Call(sample=CC2938, CallData(GT=., AD=[0, 0], DP=None, GQ=None, PL=None)), 
    Call(sample=CC3059, CallData(GT=., AD=[0, 0], DP=None, GQ=None, PL=None)), 
    Call(sample=CC3060, CallData(GT=1, AD=[0, 3], DP=3, GQ=99, PL=[115, 0])), 
    Call(sample=CC3061, CallData(GT=., AD=[0, 0], DP=None, GQ=None, PL=None)), 
    Call(sample=CC3062, CallData(GT=0, AD=[2, 0], DP=2, GQ=45, PL=[0, 45]) # etc

These can also be individually queried by sample name:

    >>> rec.genotype('CC2935')
    Call(sample=CC2935, CallData(GT=0, AD=[1, 0], DP=1, GQ=45, PL=[0, 45]))

### cyvcf2 {#cyvcf2tutorial-cyvcf2.2}

cyvcf2 takes a very different and stripped down approach to this sort of
thing.

    v = VCF(fname)
    rec = next(v)
    rec
    # Variant(chromosome_15:147 A/C)

Here are the methods available to us. Many of these should be familiar:

    >>> dir(rec)
    ['ALT', 'CHROM', 'FILTER', 'FORMAT', 'ID', 'INFO', 'POS', 'QUAL', 'REF', 
    '__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', 
    '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__le__', 
    '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', 
    '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'aaf', 'call_rate', 
    'end', 'format', 'genotype', 'genotypes', 'gt_alt_depths', 'gt_alt_freqs', 
    'gt_bases', 'gt_depths', 'gt_phases', 'gt_phred_ll_het', 'gt_phred_ll_homalt', 
    'gt_phred_ll_homref', 'gt_quals', 'gt_ref_depths', 'gt_types', 'is_deletion', 
    'is_indel', 'is_snp', 'is_sv', 'is_transition', 'nucl_diversity', 'num_called', 
    'num_het', 'num_hom_alt', 'num_hom_ref', 'num_unknown', 'ploidy', 'relatedness', 
    'set_format', 'set_pos', 'start', 'var_subtype', 'var_type']

However, instead of a Call subclass, cyvcf2 has everything bundled in
either lists or numpy arrays. This can be a bit annoying to get used to
if you made extensive use of pyVCF\'s Call objects, but is still usable.
A big problem is that sample names are not attached to individual call
information - these need to be picked out positionally using
`v.samples`, an attribute of the main iterable.

    >>> v.samples
    ['CC2935', 'CC2936', 'CC2937', 'CC2938', 'CC3059', 'CC3060', 'CC3061', 'CC3062', 
    'CC3063', 'CC3064', 'CC3065', 'CC3068', 'CC3071', 'CC3073', 'CC3075', 'CC3076', 
    'CC3079', 'CC3084', 'CC3086']
    >>> rec.gt_types
    array([0, 0, 0, 2, 2, 3, 2, 0, 2, 2, 0, 2, 2, 2, 2, 2, 0, 0, 2], dtype=int32)
    >>> rec.gt_quals
    array([ 45.,  99.,  45.,  -1.,  -1.,  99.,  -1.,  45.,  -1.,  -1.,  99.,
            -1.,  -1.,  -1.,  -1.,  -1.,  45.,  99.,  -1.], dtype=float32)
    >>> rec.gt_depths
    array([1, 6, 2, 0, 0, 3, 0, 2, 0, 0, 6, 0, 0, 0, 0, 0, 4, 7, 0], dtype=int32)

## Writing records {#cyvcf2tutorial-Writingrecords}

cyvcf2 gets some syntactic mettle back with its clean VCF-writing
syntax. Here\'s a comparison of the two:

### pyVCF {#cyvcf2tutorial-pyVCF.3}

Let\'s write a new VCF containing records with minor allele frequency \>
0.1.

    fname = 'chromosome_15.vcf.gz'

    v = vcf.Reader(filename=fname, compressed=True)
    outfile = 'pyvcf_out.vcf'

    with open(outfile, 'w') as f:
        writer = vcf.Writer(f, v) # fsock, template
        for record in tqdm(v):
            if record.aaf[0] >= 0.1:
                writer.write_record(record)

`tqdm` report:

    62699it [00:38, 1632.02it/s]

### cyvcf2 {#cyvcf2tutorial-cyvcf2.3}

    from cyvcf2 import Writer # make sure to import this!

    fname = 'chromosome_15.vcf.gz'
    outfile = 'cyvcf_out.vcf'

    v = VCF(fname)
    writer = Writer(outfile, v)

    for record in tqdm(v):
        if record.aaf >= 0.1:
            writer.write_record(record)

    writer.close()

`tqdm` report:

    62701it [00:01, 55263.37it/s]

Enjoy cyvcf2! It\'ll take some getting used to, but hopefully the
ridiculous speed upgrade is enough to convince you to ditch your pyVCF
ways.
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
