---
tags: ggg, ggg2024, ggg201b
---

[toc] 

# GGG 201b WQ 2024 - HW 1 - Links and info

Due: noon on Wed, Feb 21st, 2024.

Estimated time to complete: an hour or two.

---

## The Homework Request

On farm, in `~ctbrown/data/ggg201b`, there are four FASTQ files:

```
SRR2584403_1.fastq.gz
SRR2584404_1.fastq.gz
SRR2584405_1.fastq.gz
SRR2584857_1.fastq.gz
```

All four of them are resequencing data sets for E. coli REL606; we've been working on the last one in class.

Call variants for all four data sets using the pipeline we've been running in class, and then investigate the following questions.

You don't have to use snakemake here, but, well, it might be helpful! Note that the Snakefile has been adjusted to be useful. 

Questions:
- which variants are present in which samples?
- which variants are shared between one or more samples?
- which genes contain variants in more than one sample (and in which samples)?
- of the variants that are in a coding region, which are synonymous and which are non-synonymous?

To complete the homework, submit (via GitHub):
- any changes you made to the Snakefile
- a text file named 'hw1.txt' in which you provide answers to the above questions.

Please don't submit any of the FASTQ, SAM, BAM, GFF, or VCF files - thanks!

## The homework process

Please "claim" the assignment [here](https://classroom.github.com/a/5p0hCs34).

Then, clone the hw1 repository to your local account, as in hw0.

Do the homework!

Then, make sure your 'hw1.txt' file is in the same directory as your snakefile, and run `git add hw1.txt` and `git commit -am "changes"`. (You can do the git steps multiple times if you change the file(s).)

When you're ready to submit your homework, run
```
git push
```
to send your changes to github. (You can do this multiple times.)

Your homework is turned in when you can see your `hw1.txt` file on your github.com page.

## Tips and tricks

You'll need to copy in various files from `~ctbrown/data/ggg201b/`.

Labs 3 and 4 contain the most helpful sets of commands to look at.

Even if you don't use the Snakefile, it's got some useful commands at the bottom.

The coordinates of the coding regions are 1-based in the GFF, I believe.

## Helpful links and references

Links:
* [Lab 1](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?view) - links to UNIX shell stuff
* [Lab 2](https://hackmd.io/YJeyl2n_T9qDgdUxq57zKg?view) - basic variant calling
* [Lab 3](https://hackmd.io/dJKxykasR5aiMWHPhdiXRQ?view) - more variant calling
* [Lab 4](https://hackmd.io/brvGZewjRziahjpvr-uEqA?view) - examining variants by region; BED files; bedtools for intersections
* [Homework 0 notes](https://hackmd.io/rYDn_4Z2S2GQJKISr7fSdA?view) - how to start up RStudio, how to clone repos, how to submit via git push.

## Need help?

See the canvas page / homework announcement for details on office hours etc. You can also e-mail Titus at ctbrown@ucdavis.edu.
