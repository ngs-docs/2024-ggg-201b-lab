## Hannah's UNIX Cafe

> ### Learning Objectives
> #### Unix Learning Goals
> * Change directory and list files in directory
> * Understand basic shell vocabulary
> * Gain exposure to the syntax of shell & shell scripting
> * Download a file from the internet with `curl`
>
> #### R Learning Goals
> * Gain familiarity with the Rstudio enviornment
> * Practice using R to manipulate and analyze strings.
> * Generate an Rmd file and associated html or pdf file.

------------

### Get started
Today we're going to get familiar with the RStudio interface and the unix shell.
- Start by logging into the lab computers with your CAS (kerberos) log in, and oppening RStudio. 
- From the lab computers, log into canvas and download everything in `Files > Labs > lab_01/` folder. 
- place those files into a folder on your desktop called "bis23b" (you will need to create this folder)
- Finally open the RStudio app, and you are ready to go!


### R Studio

When you first open RStudio, you'll notice it's divided into several panels, each serving a distinct purpose.

1. **Console Panel**: This is where R code is executed. You can type commands directly here or run code from a script. It's like a direct line of communication with R.

2. **Source Panel**: Here, you write and edit files (R scripts, R markdowns, shell scripts). This panel supports features like syntax highlighting and tab-completion to make writing R code easier.

3. **Environment/History Panel**: The Environment tab displays variables created during your R session, along with their values and types. The History tab keeps a log of all commands you've run, allowing you to revisit and reuse them.

4. **Files/Plots/Packages/Help/Viewer Panel**: This multifunctional panel has tabs for:
   - **Files**: Browse, view, and manage files in your working directory.
   - **Plots**: View graphs and charts you generate with your code.
   - **Packages**: Install, load, and manage R packages.
   - **Help**: Access R documentation and help files.
   - **Viewer**: Display web content or visualizations.


#### Practice: Open the R markdown file you downloaded from canvas. it has a .Rmd extension
Discussion questions:
- What pane in R studio did this file open in? 
- Can we see the new folder, `bis23b` from the `Files` pane?

### R Markdown
This (the thing youre reading) is an R Markdown document. It combines 2 programming languages; r and markdown. 
Markdown is an formatting syntax for authoring HTML, PDF, and MS Word documents. 
R Markdown allows you to include executable R chunks (and even other languages!) among markdown formatted text. Think code & report in one place!
For more details on using R Markdown see <http://rmarkdown.rstudio.com>.


When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r}
3+5
```

More on that to come later.

#### Practice: chatGPT
Ask chat GPT to make a bullet point list of every phylum in the animal kingdom (or plant! pick your favorite kingdom :) ). 
use the *clipboard* button to copy the answer, and paste it below ...



... now try knitting!
chatgpt will store the markdown formatted text to clipboard. does it work if you just copy paste the text?




# Generating Data: Intro to the Unix Shell

## What is unix, the shell and what is the terminal?

Unix is technically an operating system, like Windows10 or MacOS. Most people are used to interacting with a graphic user interface (GUI), where you can use a combination of your mouse and keyboard to carry out commands on your computer. We can use the shell through a **terminal** program. The **shell** is a computer program that uses a command line interface (CLI) to give commands made by your keyboard to your operating system. Linux and Mac operating systems use a unix-like shell (bash and zsh, respectively), meaning they have similar commands, while windows uses a different language.

Everything we can do using our computer GUI, we can do in the shell. We can open programs, run analyses, create documents, delete files and create folders. 

We should note that _folders_ are called **directories** at the command line. For all intents and purposes they can be used interchangeably but if you'd like more information please see "The folder metaphor" section of [Wikipedia](https://en.wikipedia.org/wiki/Directory_%28computing%29#Folder_metaphor).


## Unix Shell/Terminal Introduction

Go click on the terminal "app" to get started. 

When we open up terminal in binder we will see a a line of text. This is a **prompt statement**. It can tell us useful things such as the name of the directory we are currently in, our username, or what computer we are currently running terminal on. 

However, the prompt statement that pops up is quite long, you can customize it to read `$ ` it by running:
```
PS1='$ '

```

we can clear that code from our screen with 

```
clear
```

Let's take a look around.
We can look at the contents of the current directory by using the `ls` command:

```
ls
```

This command prints out a list of files and directories that are located in our current working directory. 

Now, if we look at the contents of our current directory we have a few files, and a folder called `hannahs_unix_cafe`,

To switch the directory we are located in, we need to change directories using the `cd` command. Let's move into the `hannahs_unix_cafe` directory. 

```
cd hannahs_unix_cafe
```

We can confirm that we have moved with the **print working directory** command, which shows what directory we are currently located in.

```
pwd
```

This gives us the **absolute path** to the directory where we are located. An absolute path shows the complete series of directories you need to locate either a directory or a file starting from the root directory of your computer.

Let's have a look around.

```
ls
```
(ls stands for list. I remember it with `list stuff`)


However, this directory contains more than the eye can see! To show hidden files we can use the `-a` option.

```
ls -a
```

What did you find? 


Using options with our commands allows us to do a lot! But how did we know to add `-a` after ls? Most commands offer a `--help`. Let's look at the available options that `ls` has:

```
ls --help
```

Here we see a long list of options. Each option will allow us to do something different.


##### Practice:
Find the date `unix_cafe.txt` was created with `ls -l`



We can also combine commands:

```
ls -lah
```

This combination of options will _list_ _all_ the contents of the directory, in _"long form"_ and display file sizes in _human readable_ units between files types. 

(what does  human readable units mean? compare `ls -lah` to `ls -la`)






### Navigation
  Now we have a fairly good concept of navigating around our computers and seeing what is located in the directory we are. But some of the beauty of the shell is that we can execute activities in locations that we are not currently in. To do this we can either use an absolute path or a relative path. A **relative path** is the path to another directory from the the one you are currently in. 

Again, check out the  `hannahs_unix_cafe` directory

```
ls
```

Here we see several directories and text files. We can see what is in the text file using the `cat` command which concatenates and prints the content of the file we list. 

```
cat unix_cafe.txt
```

we can reference files by relative path too:
```
cat staff/cooks.txt
```

```
cat staff/waiters.txt 
```

Lets navigate into the `menu` directory

```
cd menu
```
and look at its contents:
```
ls 
```

We can see the contents of hours, and staff too:

```
ls ../staff
ls ../hours
```

So, even though we are in the `menu/` directory, we can see what is in other directories by using the relative path to the directory of interest. Note we can also use absolute paths too. You may have noticed the `../` this is how to get to the directory above the one you are currently located in. 

This .. feature can be used to help us navigate directories. move back up, out of the menu folder with 
```
cd ..
```

Note: in this case, we have access to the RStudio file browser, too, which is really nice. But in some situations, like if you are using a remote high performance compute cluster (hpc), you'll have to get by with just the command line interface and no other interface!

Wouldn't it be nice to see the contents of multiple directories at once? We can use a regular expression to capture a sequence of characters (like the numbers 1, 2 and 3 at the end of the tmp directories). We can use the wild card character `*`, which expands to match any amount of characters.

```
ls menu
```

```
ls menu/fall*
```

```
ls menu/*
```

We are quite used to moving, copying and deleting files using a GUI. All of these functions can be carried out at the command line with the following commands: 

Copy files with the `cp` command by specifying a file to copy and the location of the copied file. 

```
cd menu
ls
```

```
cd fall
ls
```

```
cp fall_lunch.txt fall_dinner.txt
ls
```

The syntax for the copy command is `cp <source_file> <destination_file>`. Using this syntax we can copy files to other directories as well:

```
cp year_round_offerings.txt ../spring/year_round_offerings.txt
```

If we list the files that are in the spring directory, we will see the `year_round_offerings.txt` file has been copied to the `spring/` directory.

```
ls -l../spring
```

#### Practice:

1. use that `cat` function! check out the contents of `fall_festival_specials.txt`, and 2 more menus.


2. from the `spring/` directory, copy the spring lunch menu to a spring dinner menu

3. Super Challenge: A menu was misplaced! Given that the syntax for copy is the same as the syntax for move, use the `mv` (move) command to move the `fall_desserts.txt` file from `spring/` to `fall/`.


### Copy, move, remove
Once we know how to copy and move files, we can also copy and move directories. We can create new directories with the command `mkdir`. Let's make a new directory called `winter`

```
cd ~/hannahs_unix_cafe/menu
mkdir summer
ls -l
```

The shell is quite powerful and can create multiple directories at once. It can create multiple in the current working directory:

```
mkdir winter take-out
ls -l
```

or it can create a series of directories on top of one another:

```
cd ..
mkdir -p company_secrets/lie/deep/within/the/caverns/of/unix/
```

We can use tab complete to get to the `go` directory. Type `cd h` then hit `tab`. If you hit tab enough times your command will eventually read:

```
cd company_secrets/lie/deep/within/the/caverns/of/unix/
```

You can see that we've created a bit of a monster directory structure...

you can visualize this with the tree function: 
```
cd ~/hannah_unix_cafe/
tree -L 6
```

This nicely hints at the power of the shell - you can do certain things (in this case, create a nested hierarchy of directories) much more easily in the shell. But that power cuts both ways - you can also mess things up more easily in the shell!


Now lets talk about deleting things:
```
cd ~/hannahs_unix_cafe
```

delete a file with the `rm` command:
```
rm health_report_2023.txt
```

you can delete files with their relative path too:

```
rm  hours/holiday_hours/summer_hours.txt 
```

you can delete an empty directory with `rmdir`:
```
rmdir menu/summer
```



### Intro to R programming

So far we haven't gotten into the real benefits of using an R Markdown document.
One of the greatest benefits is that you can easily embed R code, run it, make 
plots, and use all of R's functionality while creating an easy to read 
document. Let's begin with some basics. R Markdown files will automatically
interpret R code contained within chunks sandwiched by three back tick symbols.

R is basically a fancy calculator. But it can store objects such as variables or functions, which is useful. Instead of having to arithmetic over and over again, you can use functions in R to do your bidding. Let's define some objects.


```{r}
# assigning the value 3 to the variable x
x <- 3

# assigning the value 7 to the variable y

y = 7

# evaluating the sum of x and y
x + y
```

We defined two different objects here. `x` was defined as the number 3, and `y` was defined as the number 7. Note that we can assign values to a variable using either `<-` or `=`. The equals sign may seem more intuitive, but equals signs have some other meanings in other contexts in R, so we'll tend to use `<-`.  As a shortcut, you can type either `alt` and `-` or `cmd` and `-` to make the symbol `<-`, if you have a pc or mac, respectively.  

As you go through, you can use `ctrl` and `enter` to run a single line of code, or click the green play button at the right corner of the code block to run the whole block.  You can also just copy and paste into the console, but that is slow and will eventually drive you insane.

Let's define something more complicated.

```{r}
# storing a string of base pairs at the variable dna_fragment
dna_fragment <- "ACTTCTTCACGCTGCTACGTACGATATTAACGGCCGATCACGATCGACGTAGCTAGCTAGCT"
dna_fragment
```

Now we have a string stored as an object named `dna_fragment` -- a string is a 
sequence of characters. These are always surrounded by quotation marks in R.  
Even with this short string, counting the letters might get
tedious.  What functions can can R offer us?

```{r}
fragment_length <- nchar(dna_fragment)
fragment_length  #this is the total number of characters in our string
```

When you call functions in R, they will always have their argument (their input) surrounded by round brackets, (). So we can see that `nchar()` is a function. It can take a single strings as an argument, as we saw above. But it can also take a vector of multiple strings. Let's define a vector and check it out.

```{r}
# storing a vector with multiple strings
dna_fragments <- c("ATACCAT","GTTTGAGATC","CC")
dna_fragments

#counting the number of characters in each string in the vector
nchar(dna_fragments)

dna_fragments2 <- c("CCCCCCC",dna_fragments, 17)

```

Two things to unpack. First, we just used R's most fundamental function, `c()`. This creates a vector out of the entries you put inside.  Second, you just used the function `nchar()` on a whole vector, instead of a single string. Many functions in R can work with a single value, or a vector of values.  These are called vectorized functions, and they're convenient for doing a lot of work with a small bit of code.

What about the number of each of the 4 letters (our four different DNA base pairs)?
As you'll continually find out, R works better with vectors of individual characters (where each character
in the string is its own entry in an array) than it does with single strings.
Let's reformat our original string, `dna_fragment`, using the function `strsplit()`.

```{r}
#breaking a string into individual characters
dna_list <- strsplit(dna_fragment,split = "")
dna_list # this looks almost like a vector, but it's actually a list

# we can recover the vector in two ways
unlist(dna_list)  # using this function that smooshes all list entries 
# into a vector, OR

dna_list[[1]]  # it turns out the first entry in our list was a 
# a vector of characters

# let's create a new object to store this vector
dna_vec <- unlist(dna_list)
dna_vec
```
Now our data is a vector.  What have we gained?  Well, we can use some basic
R functions like `table()` to make counts of the unique entries inside. We can
easily take a subset of the vector, for example to just look at the last 6 entries.


```{r}
table(dna_vec) # a table of the counts of each unique value in the vector

dna_vec[31] # the 31st entry in the vector

dna_vec[c(1,5,12)] # the 1st, 5th, and 12th entries

dna_vec[57:62]  #the final 6 entries in dna_vec

```

Oh, the `table()` function is nice.  It counts the unique entries in a vector (and can do more complex counting too). Then we took advantage of a nice feature of vectors; it's easy to select smaller sets of entries inside.  For vectors you use the square brackets, [], and can enter a single integer or a vector of multiple integers.  The code `57:62` does exactly what you think. It makes a vector with the numbers 57,58, ...,62.

#### Practice: 
Your turn to fiddle.  Try these out on your own, and ask questions if you're getting stuck. 
```{r classwork1}
##################################
###  Your code below           ###
##################################

# create a vector named dog, consisting of the values 5, 7, 9, and 126.3
# remember to wrap the values in the c() function


# use the function mean() to calculate the mean of the vector dog


# use the command ?mean to see R's documentation of the function.
# ? before a function name pulls a useful help file.
# mean() has some extra arguments that you can use. 
# what can you do by setting a trim argument?


# below is a string stored as the object bird
# use strsplit() and table() to count the number of occurrences of the letter r
bird <- "chirp_chirp_i_am_a_bird_chirp"


###
# extra things to play with, time permitting
# check out the help file for strsplit()


# we used the argument split="" to split every character apart.
# try using strsplit() with split="_" on the variable bird.


# what is your output?  (use the # symbol at the start of the line
# to write your response as a comment, otherwise
# R will get confused when you create your final document)



# Can you imagine any scenarios where this might be useful?



##################################
##################################
```


***

__Pause here and wait for instructions on the next step.__

***

#### A first step into bioinformatics

Okay, we now have almost enough tools to do some bioinformatics. Let's compare two DNA sequences.

```{r}
# a different dna sequence (conveniently already in vector form)
dna_vec_2 <- c("A", "G", "T", "T", "C", "T", "T", "C", "A", "C", "G", "C", 
"T", "G", "C", "T", "A", "G", "G", "T", "A", "C", "G", "A", "T", 
"A", "T", "T", "A", "A", "C", "G", "G", "C", "C", "G", "A", "T", 
"C", "A", "C", "G", "C", "T", "C", "G", "A", "C", "G", "T", "A", 
"G", "C", "T", "A", "T", "C", "T", "A", "G", "C", "T")

# checking which entries are equal 
matches <-  dna_vec == dna_vec_2
matches

# adding up the matches, and dividing by the length (the number of characters)
sum(matches)/length(matches)
```

Check in with you lab neighbors.  What did we just do? What is that final value? 

We created an interesting vector called `matches` from the command `dna_vec == dna_vec_2`. It looks a little weird: a vector of `TRUE` and `FALSE`. As mentioned in the online reading, comparisons in R using symbols like `<`, `==`, and `!=` are like asking a question.  For vectors, R makes the comparison entry by entry. So `dna_vec == dna_vec_2` asked: Is the first entry in `dna_vec` the same as the first entry in `dna_vec_2`? Is the second entry the same in both? And so on. We can see that they were mostly the same, but the occasional `FALSE` values reveal places where these two DNA sequences differed. The output from this kind of comparison is a *logical vector*, so-called because we call `TRUE` and `FALSE` logical values that come from making logical comparisons betweem values.

We also took advantage of another useful feature in R. `TRUE` and `FALSE` are  equivalent to `1` and `0`, so you can find the number of `TRUE` values by just  taking the `sum()` of your logical vector. We went ahead and divided by the  `length` (the number of entries) of the vector, to get the overall fraction of the DNA sequences that were identical. This fraction comes up repeatedly during genomic analysis. It is often multiplied by 100 to become a percent, and is called *percent identity*. You will start seeing this value next week when we try to figure out which species have sequences that best match our halophile genomes.

```{r}
# Following the approach above, find the percent identity 
# for these two sequences
seq1 <- "CCTAACGTCAGCAGATCAAACGCCGATTC"
seq2 <- "CCGAAGGACTAGCTAGCTAGCGCGGATTG"

##################################
###  Your code below           ###
##################################



# After calculating it, what do you think? Are these sequences similar?
# We'll gradually get more and more context for this as the course goes on.

##################################
##################################
```



## Save your work!
make sure to save this R markdown file (.Rmd)
You will want it to complete your first report, but this version will not be graded.
You can upload to canvas under lab 1

## Lesson Sources & Resources
*You don't need to do anything here either.*
This lesson was adapted from the following resources:

- [Data Carpentries: Introduction to the Command Line for Genomics](https://datacarpentry.org/shell-genomics/)

- [DIB Lab: Advanced Beginner Shell](https://dib-training.readthedocs.io/en/pub/2016-01-13-adv-beg-shell.html)

- [ggg298 lab2: UNIX_for_file_manipulation](https://github.com/ngs-docs/2021-GGG298/tree/latest/Week2-UNIX_for_file_manipulation)
- [The sourmash portion was adapted from this  sourmash tutorial](https://sourmash.readthedocs.io/en/latest/tutorial-lemonade.html)
