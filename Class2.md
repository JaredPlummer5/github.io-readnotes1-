# Class 2

## Setting Up Your computer

In today's class we set up our computers with our terminal. This process was too long to explain here but the link below can assist you in the step by step process.

[Set Up Your Computer](https://codefellows.github.io/setup-guide/)

Please follow carefully and take your time
Once you're done please type the list one by one in your termianl to make sure everything is up to date.

- code --version
- git --version
- node --version
- npm --version
- eslint --version
- tree --version

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

`git push -u origin main` - pushes all of your changes to GitHub

![Visual of Git Pull](https://wac-cdn.atlassian.com/dam/jcr:63e58c34-b273-4e48-a6b1-6e3ba4d4a0ea/01%20bubble%20diagram-01.svg?cdnVersion=747)

### Commands for Pulling

The code below pulls things you have coded in GitHub to VScode. You will then have to push those changes in the code. There are several ways to pull changes so if these don't work google more of them.

`git pull` - will fetch the diverged remote commits which are A-B-C. The pull process will then create a new local merge commit containing the content of the new diverged remote commits

`git pull --rebase` -option can be passed to git pull to use a rebase merging strategy instead of a merge commit.

The git pull command first runs git fetch which downloads content from the specified remote repository. Then a git merge is executed to merge the remote content refs and heads into a new local merge commit.



## Text Editors and Terminal Navigation

### Text Editors

 A text editor is a piece of software that you download and install on
 your computer, or you access online through your web browser, that
 allows you to write and manage text, especially the text that you write
 to build a web site. The text editor has to be one of the most
 important tools you can use as an aspiring web developer.

Most Important Features:

  1.) code completion
  
   2.) syntax highlighting - is a feature that takes the text you type, and makes it more noticeable by colorizing the text

 3.) a nice variety of themes (to reduce eye strain and fatigue)

 4.) the ability to choose from a healthy selection of
extensions available when you need them.

#### Files

To begin with, this won't affect what we do too much but keep it in mind as it helps with understanding the behaviour of Linux as we manage files and directories.

Please make sure that when you’re saving your file, that they
have the appropriate extension at the end of the file names. For
example, your main HTML file should be called, “index.html.” Your
CSS file should be called something like “style.css.” The filename isn’t
as important as the extension (the “.html” and the “.css”).

`file` - obtain information about what type of file a file or directory is.

`ls -a` - List the contents of a directory, including hidden files.

`1. Everything is a file under Linux`
 
 `-Even directories.`

`2. Linux is an extensionless system`
 
 `-Files can have any extension they like or none at all.`

`3. Linux is case sensitive`
 
 `-Beware of silly typos.`

### Terminal Navigation

Relative path- A file or directory location relative to where we currently are in the file system.

Absolute path- A file or directory location in relation to the root of the file system.

`pwd` - Print Working Directory - ie. Where are we currently.

`ls`- List the contents of a directory.

`cd`- Change Directories - ie. move to another directory.

[Terminal Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/)

### Things I want to learn more about:

- More functions in the commnand/terminal




[Back to home page](../README.md)
