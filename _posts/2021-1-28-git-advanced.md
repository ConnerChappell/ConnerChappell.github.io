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



After adding those commits to the feature1 branch it's time to rebase and merge everything back together. Just like in the screenshot below, you would type **git branch** just to make sure you are on the right. In this case and in most cases to make things easier, you want to be on the feature branch before you rebase. Then you type **git rebase master**.

![_config.yml]({{site.baseurl}}/images/rebase/rebase6.png)



After rebasing, you are still in the feature1 branch. But now the index.html file has been added with all the commits from the master branch earlier. 

![_config.yml]({{site.baseurl}}/images/rebase/rebase7.png)



Even though we've rebased and all the commits are together on the feature1 branch, we want to perform a fast-forward merge and bring the master branch back up to where it should be. You do this by typing **git checkout master** to jump back to the master branch. From here you will merge the feature1 branch by typing **git merge feature1**. And voila, the master branch now containes all the code and commits from the feature1 branch.

![_config.yml]({{site.baseurl}}/images/rebase/rebase8.png)



As you can see you now have a streamline git history with both branches successfully merged together using rebase.

![_config.yml]({{site.baseurl}}/images/rebase/rebase9.png)


#### Interactive Rebase Example

For this interactive rebase example I went through the same commit steps as in the rebase example above. However, when it is time to rebase, instead of just typing to automated **git rebase master**, you type **git rebase -i master**.

![_config.yml]({{site.baseurl}}/images/rebase/interactive-rebase1.png)



Once the command is completed. A prompt will pop up listing all the commits that are about to be moved. It also lists different actions that can be taken for each of those commits (pick, reword, edit, squash, etc). Basically interactive rebasing allows you to alter commits as they are moved to the new branch. It offers more control over the branch's commit history. It's usually used to clean up a messy history before merging a feature branch into master.

![_config.yml]({{site.baseurl}}/images/rebase/interactive-rebase2.png)


## Git Reset, Checkout, and Revert

#### What is Git Reset?

Git Reset is one of the ways to undo changes. Basically it takes the current branch and resets it to a point (commit) somewhere else. Also, unlike git checkout, git reset moves the HEAD ref pointer AND the current branch ref pointer. In the example below we have a master branch with some commits on it. 

![_config.yml]({{site.baseurl}}/images/reset-checkout-branch.png)

Typing **git reset 25dd2f6** moves both the HEAD and branch refs to the specified commit.

![_config.yml]({{site.baseurl}}/images/git-reset/git-reset.png)

There are 3 different types of Git Reset: **- -hard**, **- -mixed**, and **- -soft**. **- -hard** resets the working directory, staging area, and commit history. This means that anything that is not comitted will be lost. **- -mixed** is the default method if you just use **git reset**. **- -mixed** affects the staging area, and the commit history. **- -soft** only affects the commit history. See the image below from Atlassian to help visualize this.

![_config.yml]({{site.baseurl}}/images/git-reset/git-reset-stages.png)

#### Git Reset Example

Below you can see all the commits I've made to a master branch. 

![_config.yml]({{site.baseurl}}/images/git-reset/reset-example1.png)

To reset to a previous commit I can use the first 7 characters of the commit hash (long set of characters). By typing **git reset - -soft 26e42c3**. Now you can see the HEAD is at the specified commit.

![_config.yml]({{site.baseurl}}/images/git-reset/reset-example2.png)

#### What is Git Checkout?

Git Checkout is another way to undo changes but not necssarilly the best. A "checkout" is basically the act of switching between versions of a target. There are 3 distinct targets which you can checkout: files, commits, and branches (which we've done above in the rebase examples). To help visualize this we will again use the master branch that was used above in Git Reset.

![_config.yml]({{site.baseurl}}/images/reset-checkout-branch.png)

Typing **git checkout 25dd2f6** moves just the HEAD ref and we are now in what's called a deatched head state. You do not want to commit when you are in a detached HEAD state.

![_config.yml]({{site.baseurl}}/images/git-checkout/git-checkout.png)

#### Git Checkout Commit Example

Again I've made some commits to a master branch in this other repo.

![_config.yml]({{site.baseurl}}/images/git-checkout/checkout-example1.png)

Now I'm going to checkout commit 3. To do this I typed **git checkout 44da408** and now it lets me know I'm in a detached HEAD state and checking out commit 3.

![_config.yml]({{site.baseurl}}/images/git-checkout/checkout-example2.png)

#### Git Checkout File Example

On a new branch I've added an index.js file and made a couple of commits. Note: if you make commits and go to checkout a file nothing really happens. After a couple of commits, I make another change and decide to now checkout the file by typing **git checkout index.js**.

![_config.yml]({{site.baseurl}}/images/git-checkout/checkout-example3.png)

#### What is Git Revert?

Git Revert is used for undoing changes to a repository's commit history. Like reset and checkout, revert takes a specified commit but does not move ref pointers like the other two. Revert will inverse the changes from that specified commit and create a new revert commit at the tip of the branch. See the images below for a visual representation. Again starting with the same master branch.

![_config.yml]({{site.baseurl}}/images/reset-checkout-branch.png)

Typing **git revert 25dd2f6** creates the new reverted commit at the tip of the branch as you can see below.

![_config.yml]({{site.baseurl}}/images/git-revert/git-revert.png)

#### Git Revert Example