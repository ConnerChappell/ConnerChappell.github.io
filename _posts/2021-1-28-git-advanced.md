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

From the research I've done, there's a golden rule that says to never use it on public branches. This is because you're changing history and things can turn for the worst depending on when and where you rebase. Also, never rebase the master branch onto another branch. More issues will happen there. 

#### Git Rebase Example

