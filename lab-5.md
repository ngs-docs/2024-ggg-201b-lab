---
tags: ggg, ggg2024, ggg201b
---

[toc]

[![hackmd-github-sync-badge](https://hackmd.io/Vs7rMLJaTHWPV8VdMND_-Q/badge)](https://hackmd.io/Vs7rMLJaTHWPV8VdMND_-Q)

# Assembly hands-on - GGG 201b WQ 2024 - Lab 5, Week 5

## Homework 1 is posted -

[Homework 1](https://hackmd.io/WJPwMTpVTcaV9K_hLCq4mw?view#)

It's due in 1 1/2 weeks. I'll hold office hours on Monday and Tuesday before, as well as answer questions via e-mail and in class next Friday.

## An assembly exercise

Working individually or in groups, please reconstruct the original text for the handouts I've given you. You may use the computer as you wish, but I suggest you avoid any attempts at programming... and **DO NOT GOOGLE THE DATA PLEASE :).**

You have 30 minutes.

Note that the handouts are available as PDF attachments on the canvas announcement for today.

Both handouts are generated from the same source text. One is short-read paired-end sequencing, the other is long-read sequencing.

Specific questions:

* what techniques or tactics are you using?
* suppose you had to do this with lots more data; how would you do it?
* what advantages do you have in this exercise (English) over DNA?
* what are the pluses and minuses of the two different datatypes?
* Does the order or organization of reads matter?
* if you get to use a reference, how do you know it’s the right reference?
    * (and what strategies might you use to validate your assembly?)
* what strategy would you use if I told you you could employ as many undergrads as you wanted to do this?

## (Discussion)

## Assembly (computational) hands on

Log into farm per [instructions](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?view#Appendix-Advance-preparation-for-HW-0---links-amp-info). I would suggest using the following `srun` command now:
```
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 8 --mem 10GB --pty /bin/bash
```

In a Terminal session, grab the assembly repository
```
cd ~/
git clone https://github.com/ngs-docs/2024-ggg-201b-assembly
cd ~/2024-ggg-201b-assembly
```

and then install a bunch of software with mamba:
```
module load mamba
mamba create -n assembly -y \
    megahit sourmash quast snakemake-minimal \
    samtools minimap2
```

This installs [the megahit assembler](https://github.com/voutcn/megahit) as well as [quast](https://github.com/ablab/quast) and [sourmash](https://sourmash.readthedocs.io/). Quast is used to calculate assembly statistics, and we will use sourmash to evaluate content overlaps between the assembly and the reads.

And then activate that software environment:
```
mamba activate assembly
```

Copy in some data:
```
cp ~ctbrown/data/ggg201b/SRR2584857_*.fastq.gz .
```

Run an assembly:
```
snakemake -j 8
```

It should take a few minutes.

What output did we get??

Now look at the quast output:
```
cat SRR2584857_quast/report.txt
```

## Evaluate how well the assembly contains the reads

First install a sourmash plugin or three:
```
pip install sourmash_plugin_containment_search \
    sourmash_plugin_abundhist \
    sourmash_plugin_venn
```

Sketch the reads and assembly into k-mers:
```
snakemake -j 2 sketch
```

Now:

Generate a Venn diagram:
```
sourmash scripts venn *.sig.zip -o assembly.png
```
and check out `assembly.png`.

Evaluate containment:
```
sourmash scripts mgsearch SRR2584857-assembly.sig.zip SRR2584857-reads.sig.zip
```

Check out an abundance histogram:
```
sourmash scripts abundhist SRR2584857-reads.sig.zip -M 100
```
