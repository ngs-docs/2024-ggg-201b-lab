---
tags: ggg, ggg2024, ggg201b
---

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
mamba create -n assembly -y megahit sourmash quast snakemake-minimal
```

And then activate that software environment:
```
mamba activate assembly
```

Copy in some data:
```
cp ~ctbrown/data/ggg201b/SRR2584857_*.fastq.gz .
```

