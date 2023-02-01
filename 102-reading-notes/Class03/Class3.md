# Class 3

## Git

## What is Git?

Git is a system of Snapshopts, Local Operations, Traking changes, Loss of Data and States .

Firstly Git USes to things in order to manage files and collaboration with a team of developers.

## CVS

The first system is called *CVCS* (Centralized Version Control System). This system is invovles a single sever storing all changes and file versions, which can allow other clinents access to them. This smoothed the collaboration process which allowed programmer to ahve more knowledge of team members' activities woth ceratin files and gave admins. more control over divvying up revision privileges.

## DVCS

The second system is call *DVCS* (Distributed Version Control systems). This system addresses the major vulnerability of the CVS: the sever as a single point of failure. If CVS crashes, collaborators can't work with each other on a file or save changes and new versions. Also if a corruption of cecentral database’s hard disk, without backing it up, all work will be lost. So DVCS allows people to create mirrored repositories. This mirror is essentially a data backups and DVCS can mirror repos. multiple times. This makes it so programmers are able to complete projects, which allows for use of various simultaneous workflows.

### Snapshots

Git is a DVCS that stores data in a file system made up of snapshot. Each time you save a changed version of your project, called commit, Git creates a snapshot of the file and stores a reference to it. If the file has not been altered, Git only stores a reference to the already-stored identical version of it.

### Local Operations

Git mostly relies on local operation because most neccessary info. can be found in local resources. This allow for process conveniency because a project's history is on the local disk. This eliminates the the need to get history info. from a server so you can keep working when not online

### Tracking Changes

Git basically detect file corruption or loss of info. in tranit since every single change applied to any file or directory is tracked by Git.

### Loss of Data

Git is set up to minimize the possibility of the corruption of files, such as accidentally lost data. Git makes it extremely difficult for a snapshot of your file that is commited to be lost.

### States

Files in Git can be in three main states: committed, modified, and staged.

- Commited means the data is securely stored in a local database

- Modified means the file has been changed but not commited

- Staged means you flagged a file's changed version to be commited in the next snapshot.

Today we learned how to connect VSCode to Github through our terminal. First we have to make a folder.

- ls

- cd projects

- ls

- cd courses

- mkdir 102

 Now we can start three step process.

- Cloning

- Commiting

- Push

Cloning is a simple process where you take the link of your repository in Github by typing the followingin your terminal.

- ls

- cd projects

- cd courses

- ls

- cd 102

## Git and VScode

1. Create a repository

- Head over to GitHub and create a new public repository named username.github.io, where username is your username (or organization name) on GitHub.

2. Clone the repository

- Go to the folder, in the terminal, where you want to store your project, and clone the new repository:
- Then use the command below by typing `git clone` and pasting the website link.

`git clone https://github.com/username/username.github.io`

3. Never Touch Code in GitHub

- Once you have done the fist two steps code in VScode only. Changing things in GitHub will cause you to do pull what you changed, accepting those changes in VScode mannually and then pushing the code.

## How to push and pull in GitHub

Pushing - updating the code you changed in VScode and putting it on the website on github

Pulling - this is for if you changed something in Github. It pulls changed from GitHub and then changes them in VScode

### Commands for Pushing

The code below pushes things you have coded in VScode to GitHub.

`git status` - tells you what you have changed

`git add --all` - adds all of your changes to the file

`git commit -m "Initial commit"` - leave a detailed commit in quotations of what you changed and why

`git push origin main` - pushes all of your changes to GitHub

![Visual of Git Pull](https://wac-cdn.atlassian.com/dam/jcr:63e58c34-b273-4e48-a6b1-6e3ba4d4a0ea/01%20bubble%20diagram-01.svg?cdnVersion=747)

### Commands for Pulling

The code below pulls things you have coded in GitHub to VScode. You will then have to push those changes in the code. There are several ways to pull changes so if these don't work google more of them.

`git pull` - will fetch the diverged remote commits which are A-B-C. The pull process will then create a new local merge commit containing the content of the new diverged remote commits

`git pull --rebase` -option can be passed to git pull to use a rebase merging strategy instead of a merge commit.

The git pull command first runs git fetch which downloads content from the specified remote repository. Then a git merge is executed to merge the remote content refs and heads into a new local merge commit.

`git push origin main` (this relays all changes to Github)

[Back to home page](../../README.md)