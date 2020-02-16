---
layout: post
title:      "My Git Guide - Workflow Instructions"
date:       2020-02-16 18:40:03 -0500
permalink:  my_git_guide_-_workflow_instructions
---



Once again Git and GitHub have dominated my thoughts and my work this week.  Writing my previous articles on [creating a proper Git repository](http://yescano.com/my_git_guide_-_steps_to_creating_a_proper_git_repository) and [using Git to collaborate with others](http://yescano.com/my_git_guide_-_guidelines_to_using_git_and_github_with_collaborators) really helped solidify my own understanding of how to use Git and GitHub in my projects.  In the last few months, I think I have really made strides in gaining a full understanding of how to use the Git commands and how to navigate GitHub.

As my Moms Can Code School cohort starts to wind down and we continue working on our final project, the importance of the proper use of Git and GitHub has really made itself clear.  Working in a team of 6 people, it can be hard to keep track of the code and files.  So, coming up with an agreed-upon set of workflow instructions is extremely helpful.  Of course this doesn’t guarantee that problems won’t arise.  Actually, there is more of a guarantee that there will be an issue somewhere down the line, but the hope is that with instructions there will always be a way to get back to a good (safe) place.

**Some things to note:**
1. The instructions I share below are designed for a team of people that are not added as direct collaborators of a project.  You must follow the initial steps to ensure proper set up before you start working.

2. Every team should make sure that they establish the proper structure and workflow that works for their team.  These instructions are meant to be a basic template. 

3. Creating new branches helps keep separation between untested features and code.  Depending on the size of the project, some teams might not care much for creating branches and might be ok with working master to master.  Neither approach is wrong - it might be a matter of preference. 

Without further ado, see the workflow instructions that could potentially save you some major headaches.

## Initial setup

1. Fork `<project>` repository to your GitHub account.
2. In the terminal, `cd` to the directory you want the new project folder to be in.
3. Clone your forked repository inside this directory by running `git clone git@github.com:<your git profile/project>.git`.
4. `cd` to the cloned project folder. 
5. Create a remote upstream to the *original* repo by running `git remote add upstream git@github.com:<original project>.git`.

Only run this initial setup once. These steps do not repeat.

## Working in a branch 

1. Run `git checkout -b <branch name>` to create a new development branch . This command also switches to the newly created branch.
2. Add some code.  Run `git status`.  Use `git status` often to know which files need to be added and committed to the code base.  You should see the following message:

```
On branch <branch name>
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

3. Run `git add <filename>` to stage your changes.
4. Run `git commit -m "<message>"`  to save your changes.
5. Run `git push origin <branch name>` to push your changes to your current development branch.
6. Once your changes have been pushed to your current development branch, go to the remote repository on github.com and create a new pull request. Make sure you are comparing your branch with the master branch from the original repository.
7. Wait until the original repository owner has merged your changes.

Repeat these steps as necessary.

## Keeping your fork in sync with original repo

1. Before you make any further changes, switch to your local master branch by running `git checkout master`.
2. To sync your master branch with the original master branch run `git pull upstream master`. (**NOTE**: Your master branch should always match the original master. All your branches should start from your master branch.)
3. Once your master branch is in sync with the remote original master, run `git push origin master` to make sure your remote GitHub repository is updated.
4. Create a new branch from the updated master branch.

Repeat these steps as necessary.

