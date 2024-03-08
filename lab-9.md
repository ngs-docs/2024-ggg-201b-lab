---
tags: ggg, ggg2024, ggg201b
---

# Quantification with RNAseq - lab 9, GGG 201b WQ 2024


## Run pipeline and install software _before_ running RStudio Server

### Allocate compute node

Log into farm with ssh, and use srun to get a compute node:
```
srun -p high2 --time=3:00:00 --nodes=1 --cpus-per-task=4 --mem=5GB --pty /bin/bash
```

### Update from github

Now, update the repo:

```
cd ~/2024-ggg-201b-rnaseq/
git pull
```

::::spoiler Do this if you didn't clone the github directory last time:

Run:
```
cd ~/
git clone https://github.com/ngs-docs/2024-ggg-201b-rnaseq
cd ~/2024-ggg-201b-rnaseq
```

::::

### Finish running quantification pipeline

Load mamba:
```
module load mamba
mamba activate quant
```
and run quantification pipeline:
```
cd ~/2024-ggg-201b-rnaseq
snakemake -j 4 -p
```

### Install RNAseq notebook environment

Next, install a notebook containing RNAseq software in R:
```
mamba env create -n rnaseq -f environment.yml
```

Q: what does this install? Take a look at [environment.yml](https://github.com/ngs-docs/2024-ggg-201b-rnaseq/blob/main/environment.yml).

(We'll be using [DESeq2](https://bioconductor.org/packages/devel/bioc/vignettes/DESeq2/inst/doc/DESeq2.html) for analysis of bulk RNAseq data.)

### Start RStudio

Now run:
```
module load rstudio-server
rstudio-launch
```
and set up your connection as normal.

::::spoiler If you are running in ondemand:

You'll need to start a new RStudio session using the `rnaseq` conda environment.
:::

## Running the RMarkdown Notebook

Using the file browser, go to the `2024-ggg-201b-rnaseq` directory in your home directory.

Click on the `rnaseq-workflow.Rmd`.

Now click on "Knit".

Wait a minute or two, and check out the popup window.

Questions to address!

* What is RMarkdown?
* What does this notebook do?
* What is the output of the quantification pipeline, and how does it get loaded into this notebook?
* What are the outputs of this notebook??

Statistics questions:

* what is the difference between pvalue and pAdj, and which should you use?
* what do we do with the outlier on the MDS plot?
* why does the MA plot look the way it does? What are the striations, and why is there a funnel?


Relevant: [green jelly beans](https://www.explainxkcd.com/wiki/index.php/882:_Significant)
