# Git Collaboration

## Objectives

1. Make a new branch for your repository using `git branch`.
2. Checkout a branch using `git checkout`.
3. Create and checkout a new branch using `git checkout -b`.
4. Create commits within a branch using `git branch`.
5. Merge branches using `git merge`.
6. Update branches from remote repositories or URLs using `git fetch`.
7. Merge updated remote branches using `git merge`.
8. Update and merge remote branches using `git pull`.

## Overview

The key to collaborating or sharing with Git is keeping discrete and individual lines of work isolated from each other. 
For example, you start work on a big feature, making a few commits that don't entirely finish the feature.

Your Git log might look like this:
```
512bec5 Still broken, working on new-feature (aviflombaum, 2 hours ago)
62d840 Almost done with new-feature (aviflombaum, 1 day ago)
fbee832 Started new-feature (aviflombaum, 2 days ago)
```
With the most recent Git log entry on top, start reading the oldest entry from the bottom of the Git log. You see two days ago we started working on our new-feature. Yesterday we were almost done. Today we made progress, but it's still broken. 

In our current state, if we had to push the repository live and deploy the latest version of our code to production, our users would see a partially finished and still broken, new-feature. That's not acceptable. The goal is to have clean code and a fully functioning user feature. What can we do? No problem, we can wait until we're done with our new-feature to deploy our code and push the repository live to our users with a few steps. 

Here's what happens. We notice a big bug (computer software error) that is currently breaking the application for all users. The bug is an easy fix. One simple change and deployment of your code can make everything work again. Unfortunately, even if you made that commit, you can't currently deploy your change because while that commit might fix the bug, you'd still be pushing your partially finished and still broken new-feature.

Your Git log might look like this:
```
r4212d1 Fix to application breaking bug (aviflombaum, just now)
512bec5 Still broken, working on new-feature (aviflombaum, 2 hours ago)
62d840 Almost done with new-feature (aviflombaum, 1 day ago)
fbee832 Started new-feature (aviflombaum, 2 days ago)
```

See, we can't push all those commits. Wouldn't it be great to isolate your new-feature work? Creating a copy of your code until it's done. So we can deploy the commit that fixes the application? You can! Using the `git branch` feature.

## Make a Branch for your Repository using `git branch`

Let's quickly make a repository that we can use as a sandbox (test environment) to experiment with the collaborative features of Git.   The concepts are included in your reading assignments but you will gain more hands-on experience of the commands by using them. Follow along by typing or copying and pasting the commands locally.

From our home directory we're going to make a new directory for our mission-critical-application.       

```
~ $ mkdir mission-critical-application
~ $ cd mission-critical-application
mission-critical-application $ git init
mission-critical-application $ touch application.rb
mission-critical-application $ git add application.rb
mission-critical-application $ git commit -m "First working version of application.rb"
```
Here's what we did:
1. Made a new directory using `mkdir mission-critical-application`.
2. Changed the directory using `cd mission-critical-application`.
3. Turned directory `mission-critical-application` into a Git repository with `git init`.
4. Created our Ruby application `touch application.rb`.
5. Programmed an entire working first version in `application.rb` (*not reflected in the CLI commands above, but we did, and it was awesome, great job!*).
6. Added our Ruby application `application.rb` to Git with `git add application.rb`.
7. Committed the first working version of our Ruby application with `git commit -m "First working version of application.rb"`.
8. Deployed your Ruby application to production and people start using it (*also not reflected in the CLI commands above, but we did, and it was awesome too, great job!*).

With our application online and customers rolling in, we notice a bug and quickly add another fix application called `first-bug-fix.rb` 

```
mission-critical-application $ touch first-bug-fix.rb
mission-critical-application $ git add first-bug-fix.rb
mission-critical-application $ git commit -m "First bug fix"
```

And could be visualized as a timeline composed of two commits.

![First Two Commits](https://dl.dropboxusercontent.com/s/ikorf1qvvp4tay0/2015-11-02%20at%2011.15%20AM.png)

## About Master Branch.

Notice the commits are occurring in a linear sequence of events, almost like a timeline. We call this timeline a branch. Whenever you are working with Git commits, you are adding commits on a timeline of code called a `branch"`.

At the start of any repository, your default branch or main timeline is called the `master` branch.

![Master Branch](https://dl.dropboxusercontent.com/s/v75as2cf6xr8n8a/2015-11-02%20at%2011.17%20AM.png)

To see the branch you are currently on type `git status`.
```
mission-critical-application $ git status
On branch master
nothing to commit, working directory clean
```
One of the responsible ways to use Git is making sure the `master` branch is always clean with working code. This allows you to add bug fixes when needed, and deploy a new application version immediately. Keeping broken code out of the master branch, always allows you to deploy the master.

## Start a New Feature using `git branch new-feature`

When starting a new feature, remember to keep the master branch clean. Always create the new feature in an isolated `feature` branch. 

Our timeline looks like this:

![Feature Branch](https://dl.dropboxusercontent.com/s/d61r0fxyriaf5oj/2015-11-02%20at%2011.52%20AM.png)

After commit 2, we branch out of the master branch and create a new timeline for commits and events specifically related to the new feature. The master branch remains unchanged and clean. Now that we've covered the idea of the new-feature branch, let's actually create it.

To create a new branch type: `git branch <branch name>`. 

In the case of a branch relating to a new feature, lets name the branch `new-feature`, like this:

```
mission-critical-application $ git branch new-feature
```

To see a list of our branches type: `git branch -a`

```
mission-critical-application $ git branch -a
* master
  new-feature
```

The `*` in front of the master branch indicates that "master" is currently our working branch. Git tells us that we also have a branch called `new-feature`. If we made a commit right now, that commit would still be applied to our "master" branch.

## Switch Branches using `git checkout`

We need to checkout or move into our `new-feature` timeline or branch. Doing this lets Git know that all commits made apply to only that unit of work, timeline, or branch. To move between branches use `git checkout <branch name>`.

Your Git log might look like this:
```
mission-critical-application $ git status
On branch master
nothing to commit, working directory clean
mission-critical-application $ git checkout new-feature
Switched to branch 'new-feature'
mission-critical-application $ git status
On branch new-feature
nothing to commit, working directory clean
```

We started on `master` branch, then checked out our `new-feature` branch using `git checkout new-feature`, thereby moving into that timeline.

Now let's make a commit for this `new-feature`. Get the feature started by making a new file called `new-feature-file` to represent the code for the new feature.

Your Git log might look like this:
```
mission-critical-application $ touch new-feature-file
mission-critical-application $ git add new-feature-file
mission-critical-application $ git commit -m "Started new feature"
[new-feature 332a618] Started new feature
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new-feature-file
```

Notice the commit we made is in the context of the `new-feature` branch.

Right as we get started on that feature, we get another bug report. Remember, the wheels of IT are constantly moving. Things happen in a heartbeat. Now we have to move back into the master branch to fix the bug and then deploy master.

Questions to consider:

1. How do you move from `new-feature` branch back to the `master` branch?

2. What will your code look like when we move back to the `master` branch? 

3. Will you see the remanents of the `new-feature` branch and code represented by the `new-feature-file`?

**Protip: You can create and checkout a new branch in one command using: `git checkout -b new-branch-name`. 
          Using `git checkout -b` creates the branch `new-branch-name` and moves the branch by checking it out.**

## Moving Back to Master using `git checkout master`

You can always move between branches with `git checkout`. Since we are currently on `new-feature`, we can move back to `master` with `git checkout master`.

```
mission-critical-application $ git checkout master
Switched to branch 'master'
```

And we could move back to `new-feature` with `git checkout new-feature`.

```
mission-critical-application $ git checkout new-feature
Switched to branch 'new-feature'
```

And back again with:

```
mission-critical-application $ git checkout master
Switched to branch 'master'
```

![Switching between branches](https://dl.dropboxusercontent.com/s/qzajqsd9f6njauc/2015-11-02%20at%2012.12%20PM.png)

From the master branch, one thing you'll notice is the code written on `new-feature`, namely the file, `new-feature-file`, is not present in the current directory.

```
mission-critical-application $ ls
application.rb first-bug-fix.rb
```

The master branch only has the code from the most recent commit relative to the master timeline or branch. The code from our `new-feature` is tucked away in the new-feature branch. Waiting patiently in isolation from the rest of our code in `master` for us to finish the feature.

Once you're on `master` you are free to make a commit to fix the bug. We'll represent this with a new file called `second-bug-fix.rb`.

```
mission-critical-application $ touch second-bug-fix.rb
mission-critical-application $ git add second-bug-fix.rb
mission-critical-application $ git commit -m "Second bug fix"
```

Let's look at our timeline now:

![Commit on Master](https://dl.dropboxusercontent.com/s/9ipgkog7yv8hrok/2015-11-02%20at%2012.18%20PM.png)

We are able to update the timeline in `master` with the bug fix without touching any of the code in our new-feature. The `new-feature` branch and timeline remains 1 commit behind the master branch, because the second bug fix commit occured in `master` and the `new-feature` branch was created only with the commits at the moment when the branch was created. You could also say `master` is 1 commit ahead of the `new-feature` branch.

Now go back into`new-feature` and complete the feature and commit. Then look at the timeline. Do you remember how to move from `master` back to `new-feature`? Let's take a look:

```
mission-critical-application $ git status
On branch master
nothing to commit, working directory clean
mission-critical-application $ git checkout new-feature
Switched to branch 'new-feature'
```

Now rename `new-feature-file` to `new-feature`. This tells the code we wrote to complete the feature and commit this change. We can rename a file with `mv <original filename> <new filename>` BASH command.

```
mission-critical-application $ mv new-feature-file new-feature
mission-critical-application $ git add new-feature
mission-critical-application $ git commit -m "Finished feature"
[new-feature bfe50fc] Finished feature
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new-feature
```

Let's look at our timeline now:

![Completed Feature Branch](https://dl.dropboxusercontent.com/s/xtoehu7tv5zim6v/2015-11-02%20at%2012.31%20PM.png)

The final step of our `new-feature` work is figuring out how to merge that timeline into the master timeline.

## Merging Branches using `git merge`

Our goal is to bring the timeline of commits that occurred on the `new-feature` branch into the `master`, so at the end of the operation, our `master` timeline looks like:

![Merged Timeline](https://dl.dropboxusercontent.com/s/bf0cktf3ag549z2/2015-11-02%20at%201.15%20PM.png)

By merging the timelines, `master` will have all the commits from the `new-feature` branch as though those events occured on the `master` timeline.

When we merge a branch with `git merge`, it's important to be currently working on your target branch; the branch you want to move into.

The first step for our `new-feature` merge is to checkout `master`. Why? Because that is where we want the commits to end up.

```
mission-critical-application $ git checkout master
Switched to branch 'master'
```

Once on your target branch, type: `git merge <branch name>` where `<branch name>` is the branch we want to merge. 

For example, type `git merge new-feature`.

```
mission-critical-application $ git merge new-feature
Updating e5830af..bfe50fc
Fast-forward
 new-feature      | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 new-feature
```

Now the branches have been merged and if you type `ls` for list, you'll see the `new-feature` file from the `new-feature` branch in your current working directory that is checked out to master.

**** need sample code ****

## Working with remote branches using `git fetch` and `git pull`

Your local branches can attach to remote branches living on the internet. Generally the branches live on GitHub, where your team members might contribute to and you can download locally.

Whenever you want to update your local copy with all the branches that might have been added to the GitHub remote, type `git fetch`.

Your Git log might look like this:
```
mission-critical-application $ git fetch
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 3), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (4/4), done.
From github.com:aviflombaum/mission-critical-application
   bfe50fc..0ae1da2  master     -> origin/master
 * [new branch]      remote-feature-branch -> origin/remote-feature-branch
```

From within `master` (though technically what branch I was in when I typed `git fetch` does not matter), I executed `git fetch`. The last 3 lines of output are really important, let's take a closer look:

```
From github.com:aviflombaum/mission-critical-application
   bfe50fc..0ae1da2  master     -> origin/master
 * [new branch]      remote-feature-branch -> origin/remote-feature-branch
```

The first line, `From github.com:aviflombaum/mission-critical-application` is informing us which remote our `git fetch` updated from, namely, the remote repository located at: https://github.com/aviflombaum/mission-critical-application

When we `fetch` with Git, we are asking to copy all changes on the remote to our local Git repository without integrating. 

The next line, `bfe50fc..0ae1da2  master     -> origin/master` is telling us that a new commit was found in `origin/master`. `origin/master` means the GitHub version of `master`. Even though Git fetched a new commit from `origin/master`, it did not merge the commit into the local master.

![Fetch without integration](https://dl.dropboxusercontent.com/s/iy2jovft8ykrxbd/2015-11-02%20at%202.08%20PM.png)

Our remote copy on GitHub has a file, `remote-bug-fix`, presumably some code that another developer pushed up to our remote version of the `master` branch to fix a bug. Even after we fetched, our local copy still doesn't appear to have that file.

After fetching, you have access to the remote code but still have to merge it. How do you merge a change fetched from `origin/master` into your current master?

From within your local master branch, type: `git merge origin/master`, referring to the branch's full path, `remote/branch`, or `origin/master`.

```
mission-critical-application $ git merge origin/master
Updating bfe50fc..0ae1da2
Fast-forward
 remote-bug-fix | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 remote-bug-fix
mission-critical-application $ ls
 application.rb		new-feature-file    new-feature		
 remote-bug-fix
```

The commits fetched via `git fetch` are now merged from the `origin/master` branch into our local `master` branch. And now `ls` reveals that the file present on the remote, `remote-bug-fix` is integrated into our local copy of `master` as well.

When we fetched, Git also output: `* [new branch] remote-feature-branch -> origin/remote-feature-branch`. Similarly, Git fetched a new branch and if we want to check it out or merge it we can using `git checkout` or `git merge`. 

Let's checkout what code is on `remote-feature-branch`, a branch another developer made for another feature, and pushed up to GitHub so they can share it with us.

```
mission-critical-application $ git checkout remote-feature-branch
Branch remote-feature-branch set up to track remote branch remote-feature-branch from origin.
Switched to a new branch 'remote-feature-branch'
```

When we checkout a remote branch fetch, Git will create a local branch to track and switch to that branch. We can now do work, push the work back up to GitHub, and another developer can fetch or bring those changes down.

Tip: `git fetch` is a low-level Git command we don't use much because it always requires two steps, first `git fetch` and then `git merge` to integrate those changes into your working branch. Generally, if you are in `master` you want to immediately `fetch` and `merge` any changes to the remote master.

## Combining `git fetch` using `git merge` by using `git pull`

If you want to both fetch and merge, which is what you'll do 99% of the time, type `git pull`. `git pull` is the combination of both `git fetch` and `git merge`.

`git pull` does the following:

1. You will `git fetch` all remote changes, including those on the current branch, existing branches, and new branches.
2. Any changes that on a remote branch that is tracked by your local branch, will be automatically merged. For example, if you are on `master` and there is a change to `origin/master`, those changes will be automatically merged.

## Conclusion

Git is complex, and collaborating with people in this manner can be challenging. There's no easy way to allow hundreds of people to work on the same code base simultaneously. These workflows are just being introduced to you.  You'll have lots of time to practice them and memorize what each command does. Don't try to learn it all at once; instead just start to get an understanding of Git's capabilities.

![XKCD Git](http://imgs.xkcd.com/comics/git.png)

<a href='https://learn.co/lessons/git-collaboration-readme' data-visibility='hidden'>View this lesson on Learn.co</a>

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/git-collaboration-readme'>Git Collaboration</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/git-collaboration-readme'>Git Collaboration</a> on Learn.co and start learning to code for free.</p>
