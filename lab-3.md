---
tags: ggg, ggg2024, ggg201b
---

[toc]

# GGG 201b WQ 2024 - Lab 3, Week 3 - Links and Info

Lab for Fri, Jan 26th, 2024

## Learning objectives for today

**Note:** I'm going to end 10 minutes early today to help people out with the homework.

Today we're going to explore:
* going from mappings to variant calling
* the impact of sequencing depth on variant calling
* 

## Log into farm, run srun. Optionally, set up RStudio.

See [Lab 2 notes](https://hackmd.io/YJeyl2n_T9qDgdUxq57zKg?view#Log-into-farm)

## Status check

You should be at a prompt that looks like this:
```
datalab-05@cpu-3-56:~$ 
```

(You might or might not be in RStudio, that's up to you.)

## Activate the `mapping` software mamba environment

Run:
```
module load mamba
mamba activate mapping
```

:::warning
Note: If `mamba activate mapping` fails, you may need to run:
```
mamba create -y -n mapping minimap2 samtools vcftools bcftools snakemake-minimal
```
:::

## Update your workflow

```
cd ~/2024-ggg-201b-variant-calling
git pull
```

:::warning
If the above returns errors, you may need to check out a copy of the github repository. Do:
```
cd ~/
git clone https://github.com/ngs-docs/2024-ggg-201b-variant-calling/tree/main
cd 2024-ggg-201b-variant-calling

cp ~ctbrown/data/ggg201b/SRR2584857_1.fastq.gz .
```
:::

## Call variants

Run the updated workflow:
```
snakemake -j 1 -p
```

This will run the commands in the `call_variants` rule, [here](https://github.com/ngs-docs/2024-ggg-201b-variant-calling/blob/main/Snakefile#L60).

This will produce a .vcf file (a variants call file). BUT! Will it be valid!? You might note the error:

>`Note: none of --samples-file, --ploidy or --ploidy-file given, assuming all sites are diploid`

:scream_cat: what do we do??

What _strategies_ are there for figuring out what to do?

Thikn about it for two minutes and/or chat with neighbors; enter your thoughts [here](https://docs.google.com/forms/d/e/1FAIpQLSdQMP9i96DDGAWrlXfQT697mC0XODm_LP1okzoOrAVkeZ0JOw/viewform).

(Fix Snakefile by editing around line 60 [view @ link](https://github.com/ngs-docs/2024-ggg-201b-variant-calling/blob/main/Snakefile#L60) & re-call variants!)

## Examining the vcf file

This will produce a file `outputs/SRR2584857_1.x.ecoli-rel606.vcf`.

If you look at the VCF file in the editor, you will see a lot of stuff at the top; or, via cat:
```
cat outputs/SRR2584857_1.x.ecoli-rel606.vcf
```

You can remove the cruft at the top with:
```
cat outputs/SRR2584857_1.x.ecoli-rel606.vcf | grep -v ^#
```

What does this ouput mean? It's ok to guess!

## Re-running variant calling on a subset of data

Let's re-run variant calling on the first 100,000 reads only:
```
snakemake -j 1 -p make_subset_vcf
```

This will produce a file `outputs/SRR2584857_1.sub100k.x.ecoli-rel606.vcf` with a LOT more rows, i.e., a lot more variants -
```
cat outputs/SRR2584857_1.sub100k.x.ecoli-rel606.vcf | grep -v ^#
```

Why?

## Why do you get _more_ variants when using _less_ data?

Talk amongst yourselves, fill in this form with your thoughts: [link](https://docs.google.com/forms/d/e/1FAIpQLScacdDjVLuqz_NOY-4f8PF6dvB7vHwad3SZLIGd9ovgoEamLA/viewform)

## Examining coverage

Run:
```
samtools coverage outputs/SRR2584857_1.x.ecoli-rel606.bam.sorted 
```

You will see:
>#rname  startpos        endpos  numreads        covbases        coverage       meandepth        meanbaseq       meanmapq
ecoli   1       4629812 2116548 4623406 99.8616 46.1237 35.2    58.5

focus in on `99.8616 46.1237` - this is how many bases are covered, and what the mean depth is.

What about when we look at the coverage stats for the subset data set?

Run:
```
samtools coverage outputs/SRR2584857_1.sub100k.x.ecoli-rel606.bam.sorted
```

and you will see:
>#rname  startpos        endpos  numreads        covbases        coverage       meandepth        meanbaseq       meanmapq
ecoli   1       4629812 99433   4048019 87.4338 2.1667  35.1    58.4

note `87.4338 2.1667`. 87% of bases only! mean depth of 2!

## Examining actual variants

Let's look at the variants in the full coverage file:
```
cat outputs/SRR2584857_1.x.ecoli-rel606.vcf | grep -v ^#
```

Pick one location (second column) and use `samtools tview` to look at it:

```
samtools tview outputs/SRR2584857_1.x.ecoli-rel606.bam.sorted outputs/ecoli-rel606.fa -p ecoli:<location>
```
and remember to replace `<location>` with the actual number.

What do you see??

Remember -
* `q` to quit
* left/right arrow to move left or right
* `.` to toggle view

What do you think you would see in the lower coverage file if you looked at some of the positions there?

## Retrenching: lots of topics :)

Let's go through some or all of:

Concepts:
* what's the goal of variant calling?
* what's the process of variant calling? mapping, pileup, calling variants
* what feature of shotgun sequencing are we taking advantage of?
* how does Illumina sequencing work?
* what impact does increased depth have on variant calling?

Practice:
* what are the actual steps of variant calling?
* why: farm; UNIX shell; srun; snakemake

Next time!

* more on VCF and stats
* exploring variants in multiple samples

## References:

[The UNIX command line](https://hackmd.io/5EfBWjCmTbWLgdC4rg8GZw?view)

[Snakemake introduction](https://ngs-docs.github.io/2023-snakemake-book-draft/)
