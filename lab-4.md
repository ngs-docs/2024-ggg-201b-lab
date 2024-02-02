---
tags: ggg, ggg2024, ggg201b
---

# Extracting and interpreting variant information - Lab 4 - GGG 201b WQ 2024

## Learning objectives

Today we'll look at how to view and interpret features on genomes using overlaps with `bedtools`!

## Log into farm, run srun. Optionally, set up RStudio.

See [Lab 2 notes](https://hackmd.io/YJeyl2n_T9qDgdUxq57zKg?view#Log-into-farm)

### Set up in Terminal:

```
module load mamba
mamba activate mapping
```

Change to the right directory:

```
cd ~/2024-ggg-201b-variant-calling
```

### view reads overlapping a particular region

http://www.htslib.org/doc/samtools-view.html

Be sure to pick a region that is big enough to include all overlapping reads.

```
samtools view outputs/SRR2584857_1.x.ecoli-rel606.bam.sorted ecoli:4530600-4530900 -o indel-4530767.fastq
```

### Viewing just a subset of variants

Let's use [bedtools](https://bedtools.readthedocs.io/en/latest/content/overview.html) to look at a subset of the variants.

Install bedtools:
```
mamba install -n mapping bedtools
```

We'll start by using `bedtools intersect` ([docs](https://bedtools.readthedocs.io/en/latest/content/tools/intersect.html)).

Create a BED file containing interval(s) of interest (see [description of format](https://genome.ucsc.edu/FAQ/FAQformat.html#format1)):
```
echo -e "ecoli\t4000000\t6000000\tend of chr" > end.bed
```

Get the intersection output in the format of the first file (BED):
```
bedtools intersect -a end.bed \
    -b outputs/SRR2584857_1.x.ecoli-rel606.vcf
```

Get the intersection output in the format of the second file (VCF):
```
bedtools intersect -a end.bed \
    -b outputs/SRR2584857_1.x.ecoli-rel606.vcf -wb
```

### Do this on a really large scale!

Let's get a table of all the genomic features:
```
cp ~ctbrown/data/ggg201b/ecoli-rel606.gff.gz .
```

This a file in the [GFF format](http://useast.ensembl.org/info/website/upload/gff.html):
```
gunzip -c ecoli-rel606.gff.gz | head -20
```

:::warning
You can download GFF files for NCBI genomes by finding their Assembly record - e.g., if you start at taxonomy, [link](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?mode=Info&id=413997), then click on "Assembly", you end up at [assembly link](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000017985.1/) and then usually I go to the three vertical dots and select the FTP site.

You can download these links with `curl -JLO <address>`.
:::

### Note, not all features are represented!?

Turns out not all of our variants overlap a gene... Can we use `bedtools closest`? [docs](https://bedtools.readthedocs.io/en/latest/content/tools/closest.html)

Run this, which will error:
```
bedtools closest -a outputs/SRR2584857_1.x.ecoli-rel606.vcf  -b ecoli-rel606.gff.gz -wb
```
with:
>Error: Sorted input specified, but the file ecoli-rel606.gff.gz has the following out of order record


So let's sort the records:
```
bedtools sort -i ecoli-rel606.gff.gz > ecoli-rel606.sorted.gff
```

And run again:
```
bedtools closest -a outputs/SRR2584857_1.x.ecoli-rel606.vcf  -b ecoli-rel606.sorted.gff -wb -d
```

But now we have another fun problem... what is it??

## Choosing just genes

The GFF file contains a few different feature types:
```
cut -f3 ecoli-rel606.sorted.gff | sort | uniq -c
```
should show:
```
   4422 CDS
      1 RNase_P_RNA
      1 SRP_RNA
      1 antisense_RNA
      2 direct_repeat
    116 exon
   4314 gene
      5 ncRNA
    184 pseudogene
     22 rRNA
      1 region
      7 riboswitch
      7 sequence_feature
     85 tRNA
      1 tmRNA
```

What do we do about this??

Let's ask ChatGPT:

[...dear ChatGPT...](https://chat.openai.com/share/fcd9c6b5-2593-486e-bd58-3d289e746923)

which gives us this command:
```
awk -F'\t' '$3 == "gene"' ecoli-rel606.sorted.gff > ecoli-rel606.gene.gff
```

This is now a GFF file that contains only the gene records! :tada: 

## OK, let's try again

```
bedtools closest -a outputs/SRR2584857_1.x.ecoli-rel606.vcf  -b ecoli-rel606.gene.gff -wb -d
```

What does this output tell us?

Q: why do we not need to sort this file?
