---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/evXh2WoORT2-4Vx5l09h5w/badge)](https://hackmd.io/evXh2WoORT2-4Vx5l09h5w)


[toc]

# Assembly, and now quantification - Lab 8 - GGG 201b WQ 2024

## What do we use assembly for?

From Lab 7 - [Why does assembly even matter??](https://hackmd.io/4c2Vyt6vQ36ALvSNHJvK_Q?view#Revisit-why-does-assembly-even-matter-maaaaaan)

## Quantifying & comparing DNA/RNA molecules in samples

So far we've used mapping to determine presence/absence of variants (+ploidy) in samples. And we've used assembly to construct new references. These are two of the three "types" of data analysis that "raw" sequencing data is used for.

What's the third? **quantification**.

This is used you have a mixture of molecules and you want to compare/contrast abundance between samples.

Shotgun sequencing + quantification applications:
- RNAseq
- ChIP-seq
- ATAC-seq
- metagenomics

### Yep

>Characterizing and comparing viral communities through envrionmental air sampling and individual sampling.

>Which pathogens have already infected my seedling? How much of the greenhouse or field that the seedling was planted in is affected by same (or different pathogens)? Is there a trend in either of the answers?

>metagenomic analysis on DNA of E.Coli infected piglets

>For example, I want to find find out how a gene of interested is regulated by other regulatory factors. At this point, Chip-seq would be a good way to do so and it will require some data sequencing. 

>I would like to use RNAseq to analyse the transcriptome of 'Cyborg cells', i.e. mammalian stem cells that have undergone intracellular hydrogelation, from Prof. Cheemeng Tan's lab, to see if and how it differs from the transcriptome of a non-Cyborg cell.

>I'm interested in compensatory transcriptomics in KO models.  RNAseq can elude to potential gene product interactions with the affected KO gene. 

>How do polyethylene terephthalate nanoparticles affect various human tissue types (epithelial, endothelial) at different locations on various genes?

>Studying epigenetic regulation of loci on a chromosome to understand how environmental factors alter gene expression.

>I would like to know about tools that identify mosaicisms either on the genetic or the epigenetic level

## The basic idea

* Create samples: mixtures of DNA (or RNA => DNA)
* Sequence randomly with (generally) Illumina or other high throughput shotgun sequencing
* Quantify molecules by mapping reads back to reference set (genome(s), transcriptome)
* Apply statistical comparisons

(whiteboarding)

## Hands-on: quasi mapping RNAseq with Salmon

Log into farm per [instructions](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?view#Appendix-Advance-preparation-for-HW-0---links-amp-info).

Load some software:
```
module load mamba
mamba create -n quant -y salmon snakemake-minimal
mamba activate quant
```

Grab some files:
```
cd ~/
git clone https://github.com/ngs-docs/2024-ggg-201b-rnaseq
cd ~/2024-ggg-201b-rnaseq
```

Execute:
```
salmon -j 1 -p
```

This workflow (see [Snakefile](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/Snakefile)):
* [grabs a bunch of sequencing data](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/Snakefile#L17)
* [downloads the yeast transcriptome](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/Snakefile#L27)
* [indexes the yeast transcriptome for use with salmon](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/Snakefile#L35) - see [salmon](https://salmon.readthedocs.io/en/latest/) docs.
* [quantifies the reads for each sample with salmon](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/Snakefile#L43)

In the end, the workflow produces `quant.sf` files that are spreadsheets of gene abundances in individual samples.

Look at
* `rnaseq/quant/ERR458493_quant/logs/salmon_quant.log`
* `rnaseq/quant/ERR458493_quant/aux_info/meta_info.json`
* and finally, `rnaseq/quant/ERR458493_quant/quant.sf`

What does this error message mean?
>Detected a *potential* strand bias > 1% in an unstranded protocol check the file
: rnaseq/quant/ERR458493_quant/lib_format_counts.json for details

look at `rnaseq/quant/ERR458493_quant/lib_format_counts.json`:
```
cat rnaseq/quant/ERR458493_quant/lib_format_counts.json
```

