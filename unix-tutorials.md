---
tags: ggg, ggg2024, ggg298, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/5EfBWjCmTbWLgdC4rg8GZw/badge)](https://hackmd.io/5EfBWjCmTbWLgdC4rg8GZw)


[toc]

# Two introductions to UNIX - GGG classes, WQ 2024

The following two resources are my recommendations for people who are relatively new to UNIX, or want a refresher. They are shorter and more focused than [Introduction to Remote Computing](https://ngs-docs.github.io/2021-august-remote-computing/) (which I also recommend, and which comes with videos - the UNIX-y bits are the first two lectures).

Please let me know at ctbrown@ucdavis.edu if you run into any problems.

## Happy Belly Bioinformatics - UNIX Crash Course

Author: Mike Lee, International Man of Mystery

UNIX crash course: [link](https://astrobiomike.github.io/unix/unix-intro)

To get started with your datalab-XX account:
1. log in & get RStudio Server up and running (tho you can also just use an ssh connection if you really want).
2. run the following commands in the RStudio Terminal (at the `datalab-xx@... : ~$ `prompt):
```
cd ~
curl -L -o unix_intro.tar.gz https://ndownloader.figshare.com/files/15573746
tar -xzvf unix_intro.tar.gz && rm unix_intro.tar.gz
cd unix_intro
```
3. Go to [Getting Started: A Few Foundational Rules](https://astrobiomike.github.io/unix/getting-started#a-few-foundational-rules) and start there!

I suggest going through at least the first two tutorials & completing "Working with files and directories", although you should skim "Redirectors and wildcards" if you can. We'll cover bits and pieces of "Six glorious commands" and "Variables and for loops" in the GGG 298, too.

## Hannah's UNIX Cafe (+ some R)

Author: Hannah Houts, UC Davis, MGG Grad Group

This is an introductory tutorial for RStudio, RMarkdown, UNIX shell, and R.

Go [here](https://github.com/ctb/hannahs-unix-cafe) and follow the directions!
