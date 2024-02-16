---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/nhAMqZ3TRgG_Hov6xxtjUQ/badge)](https://hackmd.io/nhAMqZ3TRgG_Hov6xxtjUQ)


[toc]

# Assembly hands-on - GGG 201b WQ 2024 - Lab 6

## Office hours

[Homework 1](https://hackmd.io/WJPwMTpVTcaV9K_hLCq4mw?view#) is due next Wed.

Monday is a holiday - I'll be available via e-mail. I'll be available in person at datalab from 1-2pm on Tuesday.

## Digression

What is snakemake? [link](https://ngs-docs.github.io/2023-snakemake-book-draft/)

## Assembly (computational) hands on

Log into farm per [instructions](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?view#Appendix-Advance-preparation-for-HW-0---links-amp-info).

I would suggest using the following `srun` command instead:
```
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 8 --mem 10GB --pty /bin/bash
```

In a Terminal session, grab the assembly repository:
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
snakemake -j 8 -p
```

It should take a few minutes.

What output did we get??

Now look at the quast output:
```
cat SRR2584857_quast/report.txt
```

### Assembly details and parameters

Here we're using paired end Illumina sequencing data - the R1 and R2 files. How can the assembler use this information?



## Estimate how well the assembly contains the reads

First install a sourmash plugin or three:
```
pip install sourmash_plugin_containment_search \
    sourmash_plugin_abundhist \
    sourmash_plugin_venn
```

Sketch the reads and assembly into k-mers:
```
snakemake -j 2 sketch -p
```

Here, we're decomposing the DNA sequence from the reads and the assembly into 31-base words, and then using a tricky computer science technique, sketching, to reduce the size of the k-mer sets. We can  estimate overlaps between sets based on these much smaller sketches:

To do so, run this to generate a Venn diagram:
```
sourmash scripts venn *.sig.zip -o assembly.png
```
and check out `assembly.png`. This is a view of the overlap of the distinct k-mers in the data.

Next, let's evaluate containment quantitatively, but this time let's weight by word abundance (2nd and 3rd columns):
```
sourmash scripts mgsearch SRR2584857-assembly.sig.zip SRR2584857-reads.sig.zip
```

Finally, let's examine an abundance histogram:
```
sourmash scripts abundhist SRR2584857-reads.sig.zip -M 100
```
On the y axis, we have k-mer abundance, and on the x axis, we see how many k-mers have that abundance.

Please take 5 minutes to think about these outputs, talk about them with your neighbors, and then write down why you think the plots look like they do.

[Answer using this form](https://docs.google.com/forms/d/e/1FAIpQLSeAXBJQxisxo5Jxl-fyy8-ELJbiK0ILEQNMUhTxWNl7iCasjw/viewform)

### Why k-mers?

K-mers, or k-length words, are nice because they enable reference free and also reference-dependent analyses of large sequencing data sets; in particular, it is easy for computers to determine if two words of length k are equal or not.

## Look at the actual mapping

As part of the workflow, we actually mapped the reads to the assembly! Let's take a look:

```
samtools flagstat SRR2584857_reads.x.SRR2584857_assembly.bam.sorted
```

You should see:
>4226282 + 0 primary mapped (99.22% : N/A)

wow!

But, even so, 0.78% of 4m reads is ...a lot! What can we do with these reads?

### Extracting and analyzing unmapped reads

First let's extract the unmapped reads:
```
samtools view -f 4 SRR2584857_reads.x.SRR2584857_assembly.bam -o unmapped.fastq
```

Now, sketch them with sourmash:
```
sourmash sketch dna unmapped.fastq -o unmapped.sig.zip
```
and do some comparisons.

Venn:
```

```


weighted containment:
```
sourmash scripts mgsearch unmapped.sig.zip SRR2584857-reads.sig.zip
```

histogram:
```
sourmash scripts abundhist unmapped.sig.zip -M 100
```