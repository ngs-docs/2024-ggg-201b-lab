---
tags: ggg, ggg2024, ggg201b
---

[![hackmd-github-sync-badge](https://hackmd.io/rYDn_4Z2S2GQJKISr7fSdA/badge)](https://hackmd.io/rYDn_4Z2S2GQJKISr7fSdA)


[toc] 

# GGG 201b WQ 2024 - HW 0 - Links and info

Due: noon on Wed, Jan 24th, 2024.

Estimated time to complete: less than 30 minutes, even if you watch the videos.

---

This homework is a low-stakes homework designed solely to make sure you can (a) log into farm and (b) submit future homeworks.

## Summary

* Create/log into an account on [github.com](https://www.github.com) and connect it to this assignment on GitHub Classroom by clicking [here](https://classroom.github.com/a/GuLYKzE1).
* Log into farm and start up RStudio Server [(notes)](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?both#Appendix-Advance-preparation-for-HW-0---links-amp-info), [(video)](https://video.ucdavis.edu/media/t/1_7ewrecc9).
* Generate a Fine-grained Personal Authentication Token on GitHub and clone your hw0 repository onto farm; edit `files/username.txt` to contain your UC Davis e-mail prefix, save, commit, and push. [(video)](https://video.ucdavis.edu/media/t/1_1wlln8ja)
* Verify that the `files/username.txt` has the right content on github.com under your new repository.

There is a video of starting up RStudio Server available: https://video.ucdavis.edu/media/t/1_7ewrecc9

There is a video walkthrough of the rest of this homework here: https://video.ucdavis.edu/media/t/1_1wlln8ja

## A more detailed written walkthrough

### Log into farm and start up RStudio Server

Use [these notes](https://hackmd.io/ZsRzMgMHREGWk2oGoZXOYA?both#Appendix-Advance-preparation-for-HW-0---links-amp-info).

Here's a [video](https://video.ucdavis.edu/media/t/1_7ewrecc9).

### Log into github.com

Create a new account on github.com, or log in to an existing account.

Click on https://classroom.github.com/a/GuLYKzE1,  connect your class username to your GitHub account, and accept this assignment (hw0).

Wait for your copy of the homework to be created; when you get to a page with a URL that looks like this, `https://github.com/ngs-docs/2024-ggg-201b-hw0-ctb`, you're good! (It will end with your github username, not mine ;)

## Create a fine-grained personal access token on github.com

Go to Preferences, Settings, Developer Settings.

Select "Personal access tokens", "Fine grained personal access token."

Click "generate new token".

Set the token name to something related to this class; it should be something you'll recognize.

Choose 90 days for expiration.

Select "ngs-docs" as resource owner.

Select "All repositories".

Under Permissions, Repository Permissions, change "Contents" to Read/Write.

Go down to the bottom and click "Generate token."

You should now see a page with a new token, with a name starting with `github_pat_`. Copy this entire token name and save it somewhere where you can access it again; github will not show it to you again.

## Clone your repository on github

Go to your RStudio Terminal window. Make sure you're in a Terminal, not the Console.

Type:
```
cd ~/
```
to make sure you're in your home directory.

Type 'git clone' and then paste your repository URL after it, e.g.
```
git clone https://github.com/ngs-docs/2024-ggg-201b-hw0-ctb/
```

Now paste your GitHub token in for the username and hit enter.

Leave the password empty (just hit enter).

You should, computers willing, get a copy of your github repository locally.

## Update `files/username.txt` and push changes

In the file browser window on the lower right of RStudio Server, go into your homework directory, and then `files`. Select `username.txt` and open it in the editor.

Change `username.txt` by replace `ctbrown` with your UC Davis e-mail address.

Save in RStudio.

At the terminal prompt, type
```
git commit -am "update username"
```
to commit the changes. If it says "nothing to commit", then you probably forgot to save the file in RStudio.

Now type:
```
git push
```
and it will send a copy of your changes back to GitHub. Success! You've (probably) turned in your homework!

## Trust but verify

Go to your github repository on the Web site (e.g. https://github.com/ngs-docs/2024-ggg-201b-hw0-ctb/) and verify that `files/username.txt` on there is correct.

Congratulations! You've (definitely) turned in your homework!

## Need help?

See the canvas page / homework announcement for details on office hours etc. You can also e-mail Titus at ctbrown@ucdavis.edu.
