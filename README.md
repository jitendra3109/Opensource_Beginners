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


