---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA/badge)](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA)

[toc] 

# GGG 201b WQ 2024 - Lab 1, Day 1 - Links and info

Lab for Fri, Jan 12th, 2023.

[Syllabus link](https://hackmd.io/_Z7xnCosRMKlq--I297_XQ?view)

## Schedule for lab 1

* Up front questions:
    * [What experience with R/Python scripting?](https://docs.google.com/forms/d/e/1FAIpQLSdRGuX3pC6mCwIIvL6cLFhHGJkxcB-nNwTw8Gz7xypibJQsZw/viewform)
    * [What experience with command line?](https://docs.google.com/forms/d/e/1FAIpQLSdmXtWo4lgyexBJB4zJsPgMujmUK_Wu20MlHU-em7qt7Z4B8g/viewform)
    * [What experience with sequencing data analysis?](https://docs.google.com/forms/d/e/1FAIpQLScvypAMN3MMDVZEHeT7rypXEoAOkJKch-xKUQUS1Q1aJ0S1RQ/viewform)
    * [Describe a research question that you can use sequencing data to address](https://docs.google.com/forms/d/e/1FAIpQLSe5oXCv_N4Uxl9TzoWByDfYkKOocAGdEgaycEMqB1FbBH4Beg/viewform)
* Welcome & intro
* Brief syllabus overview
* Please check that you've gotten an e-mail from me with farm account information! 
    * subject should be "farm account information for GGG 201b lab"
    * username: datalab-xx
    * password: &lt;some nonsense string&gt;
    * (if you are in GGG 298, use same account as for that class)

## Resources for learning more stuff!

### UNIX Shell specifically

For HW 0, you might find the [Happy Belly Bioinformatics UNIX Crash Course](https://astrobiomike.github.io/unix/unix-intro) helpful.

### Background campus resources on computing and bioinformatics.

You might be interested in workshops 1 through 5 of [Intro to Remote Computing](https://ngs-docs.github.io/2021-august-remote-computing/). Warning, this was written mostly by Titus ;). There are video recordings available.

You might also be interested in the Grad Pathways Microcredentialing in Research Computing - [(link)](https://gradpathways.ucdavis.edu/research-computing-pathway). Hit me up by e-mail if you're interested!

DataLab runs a bunch of [workshops](https://datalab.ucdavis.edu/workshops/) that you might be interested in, as does the [Genome Center Bioinformatics Core](https://bioinformatics.ucdavis.edu/training). The DataLab workshops are free, the GC ones are not. This course will prepare you well, and/or complement, these workshops!

The book [Bioinformatics Data Skills](https://vincebuffalo.com/book/) is an excellent reference that is worth buying if you are looking to invest ;).

## Appendix: Advance preparation for HW 0 - links & info

### Logging into farm:
    
Using the login information I sent you for farm, plese follow the appropriate set of instructions:
    
[Instructions for Mac OS, Linux, and WSL](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#mac-os-x-using-the-terminal-program)

[Instructions for Windows and MobaXterm](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#windows-connecting-to-remote-computers-with-mobaxterm)

Once you log in successfully...

You should be at a prompt that says `datalab-XX@farm:~$ `.

Things to try:`
* log out and log back in a few times to make sure you've got it! You can log out by typing `exit`.
* log in simultaneously a few times by using a new window or windows.

### Request compute resources with `srun`


Copy & paste the following command at the command prompt:
```
srun -p high2 --time=3:00:00 --nodes=1 --cpus-per-task 1 --mem 5GB --pty /bin/bash
```
This asks for three hours of access to one computer and one CPU, reserving 5 GB of memory for your use. The `-p high2` says to ask for it with high priority, while the `--pty /bin/bash` asks for an interactive terminal as opposed to running a specific program.

You should see output that looks like this:
>srun: job 9312054 queued and waiting for resources
srun: job 9312054 has been allocated resources

but with different numbers ;).

And you should end up at a prompt that looks something like this:
>`datalab-02@cpu-3-64:~$ `

but again, with different numbers.

What you've done here is **reserve** a specific chunk of compute time for your sole private use on farm. After 3 hours, your reservation will be cancelled and whatever you're running will be stopped. You can also give up your reservation early by logging out.

### Run RStudio Server on your reserved node

Now run:
```
module load rstudio-server
```
followed by:
```
module load R
```
followed by:
```
rstudio-launch 
```

The first command sets up your account to use the RStudio Server software.

The second command sets up your account to use a specific version of R.

The third command _runs_ RStudio Server on farm.

You should see output that looks like this;

>Run the following command in a new terminal on your computer:
> 
>     ssh -L50700:cpu-3-64:50700 datalab-02@farm.hpc.ucdavis.edu
> 
> Then, on your computer, navigate your browser to:
> 
>     URL: http://localhost:50700
>     Username: datalab-02
>     Password: attention-plausible-overripe-sliceable-vacant-imprint
> 
> NOTE: Using R at /share/apps/conda/environments/r-4.2.3/bin/R.

### Connect to RStudio from your laptop

Find the ssh command above that starts with `ssh -L`. We'll need to run that on your laptop, so, copy it into your copy/paste buffer.

If you're on Mac OS X, Linux, or WSL: open a new terminal prompt and paste in the command. You may need to enter your datalab password from my e-mail again.

If you're on MobaXterm, open a shell window, and paste in the command. You shouldn't need a password this time.

Leaving that all running, open a browser and paste in the URL from your ssh window. It should start with `http://localhost...`. You'll need to enter your account name and the password output by RStudio (NOT the one in my e-mail).

If all goes well... you should see an RStudio window!