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

Log into farm per [instructions](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?view#Appendix-Advance-preparation-for-HW-0---links-amp-info).

I would suggest using the following `srun` command:
```
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 8 --mem 10GB --pty /bin/bash
```

Now, install software:
```
module load mamba
mamba create -n annotation -y prokka
module activate annotation
```

Create an annotation directory for lab 7 and get the files:
```
mkdir ~/201b-lab-7/
cd ~/201b-lab-7/
cp ~ctbrown/data/ggg201b-assembly/SRR2584857-assembly.fa ./
```

Now, run [prokka](https://github.com/tseemann/prokka) to generate an annotation!
```
prokka --prefix SRR2584857_annot SRR2584857-assembly.fa
```

Honestly, reading the text output of this is fascinating in terms of understanding the process! (This is saved in the .txt file)

The important / interesting files output by prokka are:
* SRR2584857_annot.txt - summary of output
* SRR2584857_annot.err - summary of errors
* SRR2584857_annot.faa - **protein sequences**
* SRR2584857_annot.ffn - **the gene sequences**
* SRR2584857_annot.gff - **GFF file containing features!**
* SRR2584857_annot.tsv - spreadsheet of genes / annotations

Additional files:
* SRR2584857_annot.fna - the original assembly file, unchanged (but renamed :)
* SRR2584857_annot.fsa - annotated assembly file (contigs named)
* SRR2584857_annot.gbk - genbank format annotation
* SRR2584857_annot.log - log of the output
* SRR2584857_annot.sqn - not sure exactly
* SRR2584857_annot.tbl - some other format

Thought experiment - why did we not just assemble & annotate the genes from the first half of the course, rather than calling variants, for the amino acid question from homework 1?

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
