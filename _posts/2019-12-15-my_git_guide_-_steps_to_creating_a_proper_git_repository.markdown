---
layout: post
title:      "My Git Guide - Steps to Creating A Proper Git Repository"
date:       2019-12-15 23:38:57 -0500
permalink:  my_git_guide_-_steps_to_creating_a_proper_git_repository
---


I've been using Git commands for the better part of 2 years now.  I think I have a pretty good understanding of how it works.  However, every time I have to start a new project, I have to look up the steps again and again.  This post will serve as my own (and hopefully someone else's) guide to using Git from the terminal.  

****Git vs. GitHub 

The first thing we have to understand is the difference between Git and GitHub.  Simply put, Git is the tool that allows us to provide version control to our projects, while GitHub is the hosting service where our Git repositories live on the web.  You don’t need a GitHub account to use Git.  GitHub allows us to store our code and enables easy access for others to use.

**** `git init`

Before initializing a Git repository or attempting to use any Git commands make sure you have Git installed by following [these instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).  Go ahead... we'll wait.... 

![](https://i.imgur.com/6QRJFqr.gif)

Now that you know that Git is installed, let's set up the workspace.  In your terminal, make sure you are *not* working directly in the root directory.  `cd` (or change) into the directory where you want your code to live.

![](https://i.imgur.com/1L4qNYI.png)

Once you're in your chosen directory (and keep in mind that your directory of choice may be a few levels deep), create a new directory for your repository using the `mkdir <directory name>` command.  

![](https://i.imgur.com/QYmoQHV.png)

`cd` into this newly created directory by using the `cd <directory name>` command. 

![](https://i.imgur.com/wouRlnS.png)

In order to initialize this repository in Git, use the `git init` command in the terminal. 

![](https://i.imgur.com/2xpDYva.png)

You have successfully initialized your Git repository locally!  Your Git repository is ready to proceed. 


**** `git add` and `git commit`

You can create more files in this folder by using the `touch <filename>` command.

![](https://i.imgur.com/nqwYUAC.png)

Now that we've added two new files to our repository, let's check the status by using the `git status` command.  With `git status` we can see exactly the current status of our repository - which new files have been added, if existing files have been changed, or if our working branch is clean.

![](https://i.imgur.com/Ek0v8YJ.png)

As you can see the two files we added to the repository are untracked.  In order to have these files tracked by Git, we need to add them to the virtual cue of files that we want to commit.  In this case, we will use the `git add <filename>` command. 

![](https://i.imgur.com/gBfBPsn.png)

After running `git add README.md`, the README file has been added to the cue.  When you run `git status` again, you see that the README file is ready to be committed to the repository.  `index.html` remains untracked.  In other words, Git does not know of its existence; therefore, it will not save the `index.html` file to the repository until we add it to the cue. 

![](https://i.imgur.com/FzAF4R1.png)

Once the file has been added, we need to save or commit it.  For this action to take place, we need to run `git commit -m "<Brief but descriptive message>"`.

![](https://i.imgur.com/Qug8TSD.png)

We have successfully committed the README file!  Now, if we run the `git status` command once again, the README is no longer listed under untracked files or files to be committed.  We only have the `index.html` file to worry about as we have not committed the file to the repository.

![](https://i.imgur.com/LC3blzU.png)

Since this is all done locally, only you will have access to this repository and its files.  What if we wanted to make this code public?  What if we wanted to open it up to others for collaboration and contribution?  Let's find out how to do that in the next steps. 

**** `git remote` and `git push`

In order to have this repository available to other people, we will now connect it to our GitHub account.  Remember: GitHub is the online service we will use to store our repository and make it accessible to others.

For simplicity's sake, we created a new respository on GitHub, which could then be connected to the local repository.  

![](https://i.imgur.com/aJBKub9.png)

All we have to do now is run two commands in our terminal that will seemlessly make the connection for us - `git remote add origin git@github.com:<github repository>.git` followed by `git push -u origin master`.  The former makes the actual connection, while the latter pushes the changes made in the local repository up to the GitHub repository.

![](https://i.imgur.com/seahydR.png)

When we go to the GitHub repository, the README.md file is there, reflecting a full match with the changes we made in the local repository. 

![](https://i.imgur.com/b1pKl9j.png)

It worked!  We have a working local repository that is properly connected to our remote repository.  Now we can continue adding files, making sure to repeat the necessary Git commands (`git status`, `git add <filename>`, `git commit -m "<Brief but descriptive message>"` and `git push -u origin master`) in order to continuously update our remote repository with any changes made in our local repository.

![](https://i.imgur.com/JM1jLq3.jpg)

**** Conclusion

There are dozens of other Git commands that can be used in the terminal to help inform us of our code at any given time.   You may only need to use a handful of them on any given project.  As long as you understand the basic commands, these will help maintain your files and your code organized.  The commands used here are just the beginning.  In a future blog, I will guide us through the steps to using Git when working with others to ensure everyone working on the same project is on the same page at all times.  In the meantime, follow these steps, test them out on a couple of dummy repositories and take your time understanding how these commands work.  The better you know them, the easier maintaining all your future files will become.  Happy version controled coding! 
