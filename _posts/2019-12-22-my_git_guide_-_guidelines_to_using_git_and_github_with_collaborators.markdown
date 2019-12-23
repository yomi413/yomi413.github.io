---
layout: post
title:      "My Git Guide - Guidelines to Using Git and GitHub with Collaborators"
date:       2019-12-22 23:11:20 -0500
permalink:  my_git_guide_-_guidelines_to_using_git_and_github_with_collaborators
---


In my [last blog post](http://yescano.com/my_git_guide_-_steps_to_creating_a_proper_git_repository), I highlighted the steps to achieving the initialization and usage of Git and GitHub.  In this post, I want to focus on how to use Git and GitHub when collaborating with others.  It can be confusing and complicated when you don’t understand the respective relationships that collaborators and contributors have with GitHub repositories.

# ** Working With Others in Version Control Environments**

When working in a collaborative environment we must keep in mind that there are guidelines to be followed by all users.  Team collaborators and outside contributors must understand how to work with a repository to ensure an organized workflow.  The interaction we have with a repository can be of extreme significance and benefit to any project if we establish good version control, and by extension, good team work.

# ** The Difference Between Collaborator vs. Contributor**

In GitHub, our repositories live on the web where others are able to access them.  Anyone can be a contributor to your repository, especially if it is public. However, we must differentiate the access and permissions allowed between collaborators and contributors.  

Collaborators are people that a repository administrator can add to work directly in the repository.  These collaborators have full access to the repository with limited restrictions.  On the other hand, you can also have contributors to the same repository, but these people are complete outsiders to your trusted team and the project as a whole.  An outside contributor’s relationship is different than a collaborator’s relationship based on the specific permissions that have been granted to interact with a repository.

# ** How to Add Collaborators**

As we’ve established collaborators are people within your team that are building your project along with you.  

In your GitHub repository, click on the **Settings** tab. 

![](https://i.imgur.com/FJ9xZVW.png)

Once in the **Settings** tab, go to the menu provided on the left side of the page, and click on **Collaborators**. This will take you to a form prompting you to add your collaborator(s) by username, full name or email address.

![](https://i.imgur.com/OKE5Ca4.png)

An invitation is generated and emailed to your collaborator(s).  Once they accept the invitation, they will be able to work freely in your repository.

# ** To Fork or Not To Fork**

When you are added as a collaborator you don't have to fork the repository you have been added to.  As a collaborator, you have been given permission to interact directly with the repository.  However, as a contributor, because you don't have the same permissions, you have to interact with the repository differently.  This is where forking plays a major part. 

When you fork a repository you are making an exact replica of said repository on GitHub.  Once that version exists in your GitHub account, you then clone it to your local environment where you can freely interact with it in isolation of the original remote repository.  If a contributor attempts to make changes to a repository without forking it first, the terminal message will look as follows:

![](https://i.imgur.com/vMy9HO7.png)

So let’s break it down a bit.  I had cloned the above repository without first forking it.  I made changes to the cloned version that now exists in my local environment.  When I attempted to push the changes to the remote repository the error message inside the rectangle above was printed to the terminal.  Without forking we have no actual connection to a remote repository to push any changes to.  This step cannot be forgotten by a contributor.

# ** An Important Note on Branches**

One very important thing we have not addressed is the use of branches in order to separate the tasks and features that collaborators work on.  It’s good practice to create new branches before adding anything or making changes to the working repository. Branches allow for the isolation of development work.  Once changes have been made to a separate branch, the collaborator can submit a pull request and await approval of changes.  This allows for the repository administrator to maintain control over the master branch.  The master branch should be left for the organization of finalized code and features as much as possible.  

# ** Updating Your Local Repository** 
When working with others, you must ensure that you are always working with the most up to date project possible.  Before making any changes affecting the remote repository, a collaborator must run `git pull` in the terminal.

![](https://i.imgur.com/IkxGRim.png)

`git pull` is the combination of two different commands - `git fetch` and `git merge`.  With `git pull` all changes made to the remote repository are now included in your local copy.  Now you can make all of your changes, and add, commit and push them onto the remote repository. 

Running `git pull` is also just good practice.  If no changes have been made to the remote repository and you run `git pull`, you will see the following in your terminal:

![](https://i.imgur.com/NH3to5f.png)

At least you’ll know that your repository is the same as the repository in GitHub. 

# ** Conclusion**
The use of Git and GitHub when working with others has proven to be of utmost importance when working collaboratively.  Whether you’re a collaborator or an outside contributor, knowing how to interact with a repository on GitHub will hopefully save you time and headaches when working on your projects.  Remembering to follow some of these guidelines takes time and practice.  Don't be discouraged - eventually interacting with Git and GitHub will become second nature.  










