---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/YJeyl2n_T9qDgdUxq57zKg/badge)](https://hackmd.io/YJeyl2n_T9qDgdUxq57zKg)

[toc] 

# GGG 201b WQ 2024 - Lab 2, Day 2 - Links and info

Lab for Fri, Jan 19th, 2024.

(Homework note! It is broken! I am fixing! Apologies!)

## Learning objectives for today

Today we are going to do our first hands-on mapping! This will involve a lot of things - logging into farm, requesting a compute node, installing software, grabbing a workflow, copying data, and then actually running the workflow. We'll end by inspecting the output.

It is totally ok to be overwhelmed. We'll revisit different parts of this over the next few weeks and I'll provide links for those who want more detail on what's going on.

For all of this we will be typing commands at the UNIX shell, so you might want to look through [these introductions](https://hackmd.io/5EfBWjCmTbWLgdC4rg8GZw#) in your free time.

## Log into farm

You can use RStudio, or you can just use ssh or MobaXterm to log in to farm.

The main piece of _information_ you need is in the e-mail with the subject "farm username and password for GGG 298". You should have received this e-mail last week. If you aren't officially signed up for the course, please drop me a note at ctbrown@ucdavis.edu right now, and I'll give you one!

Once you have this information, please follow the relevant instructions below:

[Instructions for Mac OS, Linux, and WSL](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#mac-os-x-using-the-terminal-program)

[Instructions for Windows and MobaXterm](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#windows-connecting-to-remote-computers-with-mobaxterm)

## Run srun if you are not using RStudio

```
srun -p high2 --time=2:00:00 --nodes=1 --cpus-per-task=4 --mem=5GB --pty /bin/bash
```

## Status check

You should be at a prompt that looks like this:
```
datalab-05@cpu-3-56:~$ 
```

## Commands

Load the `mamba` software module that lets us use `mamba` to install software:
```
module load mamba
```
(For more information on `mamba` and the conda software installation system, see: [the conda section of the remote computing tutorial](https://ngs-docs.github.io/2021-august-remote-computing/). Videos are available!

Install the software to do basic mapping ([minimap2](https://github.com/lh3/minimap2)), work with the output files from mapping ([samtools](http://www.htslib.org/)), and investigate or call variants ([vcftools](https://vcftools.github.io/index.html)).

We are also going to use [the snakemake workflow system](https://snakemake.readthedocs.io/en/stable/) to manage running these tools:
```
mamba create -y -n mapping minimap2 samtools vcftools bcftools snakemake-minimal
```

Then activate the environment:
```
mamba activate mapping
```

Get a simple snakemake workflow:
```
cd ~/
git clone https://github.com/ngs-docs/2024-ggg-201b-variant-calling
```
Note that you can ask ChatGPT to give you the commands in here if you like - [transcript](https://chat.openai.com/c/72aa781f-0c8d-42ff-b9fc-dea98140a565).

Change your current working directory to the newly created git repository:
```
cd ~/2024-ggg-201b-variant-calling
```

## Status check 2

You should be at a prompt that looks like this:
```
(mapping) datalab-05@cpu-3-56:~/2024-ggg-201b-variant-calling$ 
```

* If you have `farm` in your prompt and don't have `cpu-XXX` there, you need to do the srun.
* If you don't have 'mapping' in the prompt, you need to `module load mamba` and `mamba activate mapping`
* If you don't have `2024-ggg-201b-variant-calling` in the prompt you may need to do the git clone and/or `cd` command

## Do a mapping!

Copy in sample data:
```
cp ~ctbrown/data/ggg201b/SRR2584857_1.fastq.gz .
```
This is data downloaded from [the Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra).

Inspect the data file:
```
gunzip -c SRR2584857_1.fastq.gz | head
```
This is a [FASTQ](https://en.wikipedia.org/wiki/FASTQ_format) file, which is a common format used for Illumina shotgun sequencing data.

Copy in the reference genome:
```
cp ~ctbrown/data/ggg201b/ecoli-rel606.fa.gz .
```
Downloaded from [here](https://www.ncbi.nlm.nih.gov/Taxonomy/Browser/wwwtax.cgi?mode=Info&id=413997).

Inspect the first few lines:
```
gunzip -c ecoli-rel606.fa.gz | head
```
This is a [FASTA](https://en.wikipedia.org/wiki/FASTA_format) file, compressed by [gzip](https://en.wikipedia.org/wiki/Gzip).

Map the reads to the reference genome by running the workflow in [`Snakefile`](https://github.com/ngs-docs/2024-ggg-201b-variant-calling/blob/main/Snakefile) with snakemake:
```
snakemake -p -j 4
```

This workflow:
* uncompresses the reference genome using gunzip;
* uses minimap2 to map the reads to the reference genome, producing a SAM file;
* uses samtools to convert the SAM file into a BAM (binary) file that can be queried more efficiently;
* uses samtools to sort and then index the BAM file;

Next week we will call variants! But for now let's just look at the files.

## List of output files

You can use
```
ls -1 outputs/
```
to get a list of files in the outputs directory. It should match what you see in the folder displayed by RStudio's file view, if you are running RStudio; or what you see in the file sidebar of MobaXterm if you're using that.

```
SRR2584857_1.x.ecoli-rel606.bam
SRR2584857_1.x.ecoli-rel606.bam.sorted
SRR2584857_1.x.ecoli-rel606.bam.sorted.bai
SRR2584857_1.x.ecoli-rel606.sam
ecoli-rel606.fa
ecoli-rel606.fa.fai
```

## Inspect the SAM file - what is what?

Google: "what are the columns in a SAM file" ;)

Look at the SAM file:
```
head outputs/SRR2584857_1.x.ecoli-rel606.sam
```

Note that the BAM files are not text but rather binary and can't be visualized by `head`.

Highlights:
* `SRR2584857.1` is the read name
* `ecoli` is the chromosome name (reference genome)
* 3075150 is the location the read maps to
* 60 is the mapping quality
* 101M is called a CIGAR string - here, '101M' means that 101 bases matched.

Questions to discuss:
* what order are the locations in? Why?

## Examining the output

Visualize the output with `samtools tview`:
```
samtools tview outputs/SRR2584857_1.x.ecoli-rel606.bam.sorted outputs/ecoli-rel606.fa
```
This opens up an interactive text viewer for the mapping. The first line is the position in the reference genome; the second line is the reference sequence; and below that are all of the reads that map. "." means the read matches to this location in a forward direction, while "," means the read matches the reverse complement. A letter of DNA means there is a mismatch.

You can use the following commands here:
* `q` to quit
* left/right to pan left or right
* `.` to toggle view between consensus view and sequence view
* `g` to go to a new location

Scroll around a bit!

* What position did we start at? Why?
* Type 'g' and edit the number to go to location 3930980. What do you see?

Generate some simple statistics:
```
samtools flagstat outputs/SRR2584857_1.x.ecoli-rel606.bam
```

You should see:

```
2129974 + 0 in total (QC-passed reads + QC-failed reads)
2129833 + 0 primary
0 + 0 secondary
141 + 0 supplementary
0 + 0 duplicates
0 + 0 primary duplicates
2116548 + 0 mapped (99.37% : N/A)
2116407 + 0 primary mapped (99.37% : N/A)
0 + 0 paired in sequencing
0 + 0 read1
0 + 0 read2
0 + 0 properly paired (N/A : N/A)
0 + 0 with itself and mate mapped
0 + 0 singletons (N/A : N/A)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)
```

A key line:
```
2116548 + 0 mapped (99.37% : N/A)
```

So some number of reads aren't mapping! What's up??

[Question: why might reads not map to the reference genome?](https://docs.google.com/forms/d/e/1FAIpQLSeztc5e8tCigD9Cez-UOV9NnEXvwMdrsp01bpAuGDAbpKo0oQ/viewform)

## Summary of today

Today we:

* logged into farm
* requested a compute node for ourselves with srun
* installed some software with conda
* grabbed a simple variant calling snakemake workflow off of github
* ran the mapping part of the workflow
* explored the mapping output

Whew, this was a lot!

Next week we'll retrench a little bit, revisit some of these commands, and explore the concepts of shotgun sequencing and mapping, before moving on to talking about variant calling.

