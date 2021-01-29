---
layout: post
title: Git - Advanced
---

## Git Rebase

#### What is Git Rebase?

Git Rebase is one of the two ways to integrate changes from one branch onto another (the other way being merge). It rewrites the project history by creating brand new commits for each commit in the original branch. Everything is essentially brought together on a single branch. The images below should help visualize what is happening when you use git rebase. 

In this first image we have a project with an original (master) branch that has some commits on it and a feature branch which has some commits.

![_config.yml]({{site.baseurl}}/images/rebase/git-rebase-visual1.png)

This second image shows what happens after we use git rebase. You'll want to make sure you checkout to your feature branch first. From there you enter **git rebase master** in the command line. Those original commits on the feature branch have been moved onto the tip of the original (master) branch. The project history has been rewritten.

![_config.yml]({{site.baseurl}}/images/rebase/git-rebase-visual2.png)

#### Advantages of Git Rebase

- Streamlines for a cleaner project history
- Avoids the potential mess of repos with lots of branches and merges

#### Disadvantages of Git Rebase

- Rewriting history can be dangerous for team collaboration and workflow
- You can lose the context provided by a merge

#### When shouldn't you use git rebase?

From the research I've done, there's a golden rule that says to never use it on public branches. This is because you're changing history and things can turn for the worst depending on when and where you rebase. Also, never rebase the master branch onto another branch. More issues will happen there. And finally, if you are working with others on a remote repo, always use **git pull** before you rebase. If you don't and they've already made commits to the master branch, everything is going to diverge and be out of sync. You're going to lose work.  

#### Git Rebase Example

> All of the text in this section will be describing the screenshots directly underneath them. 

You'll initlize your repository and make an initial commit. This will be on the master branch. As you can see below, an index.html file was added for the initial commit. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase1.png)

Now the initial commit has been made (could be more than one commit in a real project) and you want to add a feature. To work on this feature separately, a branch called feature1 was created. However, because only checkout was used, we are still located on the master branch. You can see what branch you're on including all of the branches in the repo by typing **git branch**. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase2.png)

Now let's say just for example purposes, while you're working on the feature1 branch, a couple of team members have been updating the code on the main branch and making commits. In the screenshot below you can see that 2 commits have been made on the master branch: some starter code was added and an h1 was also added to the body. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase3.png)

For you to work on the feature1 branch you must jump over to it by typing **git checkout feature1**. As you can see, no code has been added since this branch was created based off the initial commit earlier. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase4.png)

Now you make 2 commits to this branch by adding an index.js file and then some code to that file. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase5.png)

After adding those commits to the feature1 branch it's time to rebase and merge everything back together. Just like in the screenshot I would type **git branch** just to make sure you are on the right. In this case and in most cases to make things easier, you want to be on the feature branch before you rebase. Then you type **git rebase master**.
![_config.yml]({{site.baseurl}}/images/rebase/rebase6.png)

After rebasing, you are still in the feature1 branch. But now the index.html file has been added with all the commits from the master branch earlier. 
![_config.yml]({{site.baseurl}}/images/rebase/rebase7.png)

Even though we've rebased and all the commits are together on the feature1 branch, we want to perform a fast-forward merge and bring the master branch back up to where it should be. You do this by typing **git checkout master** to jump back to the master branch. From here you will merge the feature1 branch by typing **git merge feature1**. And voila, the master branch now containes all the code and commits from the feature1 branch.
![_config.yml]({{site.baseurl}}/images/rebase/rebase8.png)

As you can see you now have a streamline git history with both branches successfully merged together using rebase.
![_config.yml]({{site.baseurl}}/images/rebase/rebase9.png)

#### Interactive Rebase Example
