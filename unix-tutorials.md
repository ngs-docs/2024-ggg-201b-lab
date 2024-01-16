---
tags: ggg, ggg2024, ggg298, ggg201b
---

[toc]

# Two introductions to UNIX

## Hannah's UNIX Cafe (+ some R)

Author: Hannah Houts, UC Davis, MGG Grad Group

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
3. Go to [A Few Foundational Rules](https://astrobiomike.github.io/unix/getting-started#a-few-foundational-rules)!

I suggest going through at least the first two tutorials & completing "Working with files and directories", although you should skim "Redirectors and wildcards" if you can. We'll cover bits and pieces of "Six glorious commands" and "Variables and for loops" in the GGG 298, too.
