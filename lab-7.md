---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/4c2Vyt6vQ36ALvSNHJvK_Q/badge)](https://hackmd.io/4c2Vyt6vQ36ALvSNHJvK_Q)


[toc]

# Annotation hands-on - GGG 201b WQ 2024 - Lab 7

Note: if you see your homework on github, I see it :). And, conversely, if you _don't_ see it there... I don't either.

## Visual exploration of genomic data

First half of class: Dr. Daniela de Soto, [Visual exploration of genomic data with the Integrative Genomics Viewer (IGV)](https://hackmd.io/xtPqCSlvQNyLCWwMJ0ctuw)

## Annotating your assemblies

*Alt: Mommy, where do GFF files come from?*

@@ rstudio login

```
module load mamba
mamba create -n annotation -y prokka
module activate annotation
```

@@ create directory, get files - datalab-08

```
prokka --prefix SRR2584857_annot SRR2584857-assembly.fa
```

@@ look at output, examine gff

### Annotation basics

Genome annotation is almost entirely based on:
* simple models of genes, e.g. open reading frames (ORFs);
* homology (inferred by sequence similarity) using either BLAST or HMMER;
* other data sets (especially: RNAseq)
* less reliable: eukaryotic gene finders

### How annotation differs in euks and bacteria/archaea/viruses

tl;dr Introns suck.

Bacterial and viral gene prediction mostly Just Works, except when biological weirdness gets in the way (e.g. alternate amino acids).

If you are annotating the genes in a eukaryotic genome, *especially* one with no close relatives that are well annotated, you will almost always want good comprehensive RNAseq.

Here one big problem is that RNAseq is always of a particular tissue/mixture of tissues/life stage, so genes that are not expressed then/there won't be represented. There is also the problem that transcription from the genome is pretty noisy, so there are a lot of places that are transcribed but that (don't seem to be) genes. Often, protein-coding is used as a filter.

This is where you

But if you _just_ use sequence similarity, you almost always miss UTRs.

So it always ends up being a mixture of computational techniques.

Check out the following two papers for the actual process used to construct genes anotations from data -

* Figure 1 of [Tissue resolved, gene structure refined equine transcriptome](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-016-3451-2)
* Figure 1 in [Identification of long non-coding RNA in the horse transcriptome](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-017-3884-2)

## Revisit: why does assembly even matter, maaaaaan?

### Yep:

>Characterizing and comparing viral communities through envrionmental air sampling and individual sampling.

>My last rotation project utilized long read sequencing reads to generate haplotype assemblies for the two parents and then aligned short read sequencing data for 40 F1 individuals to the haplotype assemblies. I utilized these data to begin delineating the sex determining region in pistachio. 

### Maybe:

>Which pathogens have already infected my seedling? How much of the greenhouse or field that the seedling was planted in is affected by same (or different pathogens)? Is there a trend in either of the answers?

>Are variants in hidden/dark duplicate genes different between autistic and control individuals in a way that is contributing to the disease?

>metagenomic analysis on DNA of E.Coli infected piglets

>figuring out if an endangered species is or could be in danger of hybridizing. Also if the hybridization could be harmful to its fitness

### Probably not:

>Tracking mutations within an organisms genome

### What distinguishes these situations?

What makes assembly-based approaches a necessity? Any ideas? :)
