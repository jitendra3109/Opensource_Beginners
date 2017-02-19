# Opensource_Beginners
## How to contribute on Open source via Github for beginners guide.
 This guide containing the step by step work which can help you to overcome your first scary fear so,Let's get start.
 Before we start I assume you have git on system if not then first install [Here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

 ##Table of Contents:

1. [Read a GitHub Repository](#reading-a-github-repository)
1. [Forking A GitHub Repository](#forking-A-github-repository)

2. [How to connect/update with original project / Setting up remote connection?](#setting-up-remote)

3. [Working with Branches](#setting-up-a-branch-and-working-with-it)

4. [How to resolve Merge conflicts?](#merge-conflicts) 

5. [Squashing Commits](#squashing-the-commits)

6. [Submitting a Pull Request](#submitting-a-pull-request)

7. [How to re-name the commit message after push?](#renaming-a-commit-message-after-push)

8. [How to undo commits?](#permanently-removing-commit-from-remote-branch-/-revert-a-commit-already-pushed-to-a-remote-repository)

## Reading a Github repository

Basically read the Readme.md file carefully after I'm sure you find overall idea of project.
There is also one file contribute.md file,Please read also carefully if you want impresive contribute. 


## Forking A GitHub Repository

Forking it is basically making a copy of the repository,It also provide a link with the original repository. 

Forking a repository:

1. Make sure you’re logged into GitHub with your account.
2. Search the repo name with the different language or most active repo etc.
3. Find the GitHub repository with which you’d like to work.
3. Click the Fork button on the upper right-hand side of the repository’s page.
4.After that take it locally on your system through git clone.
Using this command ->
`git clone <your ssh/git url from right side green button just click on it and it will copy auto and peste here ctrl+shift+v in ubuntu >`

##Setting up remote

Git already added a Git remote named origin to the clone of the Git repository on your system, and this will allow you to push changes back up to the forked repository in your GitHub account using git commit (`git commit -m "massage"`) and git push(`git push`) .
To add a Git remote pointing back to the original repository (the one you forked on GitHub) , like this:

` git remote add upstream <your ssh/git url> `

This will add the original project as a remote named 'upstream'. To get/update the code, type:

` git fetch upstream `

Then, to merge it into your own project, type:

` git merge upstream/master `

Now you'll have an up-to-date version of the upstream code in your current branch.
and push again (`git push origin <branch name>`)

##Pushing changes to GitHub 

So let’s say you’ve made the changes necessary to implement the specific feature or enhancement and you’ve committed the changes to your local repository throgh (`git commit -m "massage"`).The next step is to push those changes back up to GitHub.

If you were working in a branch called branch-name, then pushing the changes you made in that branch back to GitHub would look like this:

`git push origin <branch-name>`

If your work only master

`git push origin master`


##Merge Conflicts

**Merging** is the act of integrating another branch into your current working branch. While working on a shared project sometimes it happens that two people changed the same lines in that same file, or one of the person decided to delete it while the other person decided to modify it, _Git_ simply cannot know what is correct. So it marks the file as having a conflict - which we'll have to solve before we can continue our work.

A typical merge conflict message looks like this:

`$ git checkout newfeature`

`Switched to branch 'newfeature'`

`$ git merge master`

`Auto-merging filename.java`

`CONFLICT (content): Merge conflict in filename.java`

`Automatic merge failed; fix conflicts and then commit the result.`

When faced with a merge conflict, the first step is to understand the reason behind the conflict. Git tells you that you have "unmerged paths" (which is just another way of telling you that you have one or more conflicts) via "git status" which looks like this :

`$ git status`

`On branch newfeature`

`You have unmerged paths`

`(fix conflicts and run "git commit")`


`Unmerged paths:`

`(use "git add <file>..." to mark resolution)`


      `both modified: filename.java`


`no changes added to commit (use "git add" and/or "git commit -a")`


Now it's the time to have a look at the contents of the conflicted file. Git marks the problematic area in the file by enclosing it in `<<<<<<< HEAD" and ">>>>>>> [other/branch/name]`.

The contents after the first marker originate from your current working branch. After the angle brackets, Git tells us where (from which branch) the changes came from. A line with "=======" separates the two conflicting changes. Our task is to identify and decide which piece of code is required and which is to be removed.


###Resolving merge conflicts after the PR has been sent without creating a new commit  

Many times while working, we feel the requriment of updating our code, so that we can have an up-to-date version of the upstream code in our current branch. During the process of merging the two codes, the one on which we are working and the another which has been fetched from the remote, Git creates a commit by itself which looks like this: 

`Merge master into newfeature.`

 Also, you submitted a Pull Request to the main repository but before the request could be merged, changes were made in the repository and now your PR presents merge conflicts. You could fetch the work, resolve merge conflicts and push again but that will lead to `MERGE COMMIT` which you don't want to create because Git doesn't allow rebasing for merge commits so there is no way to rebase it into the previous commit.
 
So, to avoid this you have to follow the following steps:

- Checkout your branch on which you want to update the code

`git checkout newfeature`

- Fetch the changes from the upstream code

`git fetch upstream`

- Remove/Stash any local changes, if any 

`git stash`

- Rebase to the latest branch in upstream (let say master in this case)

`git rebase upstream/master`

And suppose in between any merge conflicts occur then 

- Fix the conflicts in the project then add the files by using 

`git add <file name>` or `git checkout -- <file name>`

- After the changes have been fixed run 

`git rebase --continue`

Now the changes from the upstream have been applied and the work/ local changes you made has been applied on top of it

- Force push to your branch to update the PR by using

`git push --force origin newfeature`

###Undoing a merge

You can return to the state before you started the merge at any time like this: 

`git merge --abort`

or in case you've made a mistake while resolving a conflict and realize this only after completing the merge, you can still easily undo it like this:

`git reset --HARD`

It just roll back to the commit before the merge happened and start over again.


##Squashing the commits

Often while working on a feature you might create multiple commits but usually it is expected to submit entire feature change is in the form of one single commit before sending pull request back upstream. To squash all the commits into one we do rebasing. 

First, you need to take a look at the commits you've made with `git log` and figure out the commits that you want to squash. If you wanted to squash the into one, you'd open up an an interactive rebase like this:

` git rebase -i HEAD~3`

where -i is for interactive rebase
      ~3 stands for the number of commits you want to squash
      
The above command will bring you into your editor with some text that will look something like this:

`pick df94881 Allow install to SD` 
 
`pick a7323e5 README newfeature`

`pick 3ead26f rm classpath from git` 

To squash those commits into one, change to something like this:

`pick df94881 Allow install to SD` 
 
`squash a7323e5 README newfeature`

`squash 3ead26f rm classpath from git` 

Then, save/quit, and you'll be brought to into another editor session, describe the changes as well as you can and save/quit again. Now you're commits are squashed into one and you're ready to submit a `pull request`.


##Submitting a Pull Request

Once you've commited and squashed your changes, push them to your remote like this:

`git push origin newfeature`

Once you push a new branch up to your repository, GitHub will prompt you to create a pull request (assuming that you’re using your browser and not the GitHub native apps). The maintainers of the original project can use the pull request to pull your changes across to their repository and, if they approve of the changes, merge them into the main repository.

Then, click on the little button that says 'Pull Request'. This will bring you to a page asking you to describe your change. Describe it thoroughly.


##Renaming a commit message after pushed

Sometimes after sending a pull request you just realised that the you've made an error while writing a commit message and the project maintainer has asked you to rename it which you can do like this:

`git commit --amend -m "New commit message"`

and then to push it back to the upstream and update your pull request which can be done like this:

`git push --force origin newfeature`