# Git Rebase with Squash

`git rebase` enables you to modify your commit history in a variety of ways. For example, you can use it to reorder commits, edit them, squash multiple commits into one, and much more.

![image](https://user-images.githubusercontent.com/5396174/188719783-3788edc0-0caa-40cb-a0ae-56c336f69a7c.png)


To enable all of this, rebase comes in several forms. In this section, we will explore basic rebase, rebase with interactive option, and rebase with squash.

Why would you want to use `git rebase`? The goal of rebase is similar to that of `git merge`: they are both trying to integrate one branch to another. Now, if you are using web based git platforms like GitHub, GitLab, or BitBucket, you are maybe familiar with the concept of **Pull Requests** or **Merge Requests**. `git merge` or `git rebase` provides a similar way to merge one branch with another but through a plain simple git way. 

Merge works by creating a new commit in a destination branch by tying together the histories of both branches, and it is a safe operation. 

Rebase, in other hand, moves the entire commits, though there is a selective way to choose, to the tip of destination branch. This essentially re-writes the project history.

## Exercise - Git Rebase

We will go through an exercise to try to out `git rebase`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: You can continue to use a same directory and a same script for other continuing exercises. However, the idea is to allow users to pick up from any step that they want to review later without depending on other steps. In addition, it is always easy to work with a clean slate. Because of this, you will see same or similar commands and instructions getting copied over multiple time.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitRebaseDemo`
mkdir GitRebaseDemo
# Go inside the directory
cd GitRebaseDemo
```

### STEP 2: Create a new file to initialize git structure

> NOTE: This script is little different from script used for `git revert` and `git commit --amend`. However, this script can be used for other scenarios as well.

Create a new file called `generate-git-multiple-branches.sh`. You can do it with either by going inside a directory and create a file through a tool like **Visual Studio Code**. Or, you can use a tool like **VIM** to quickly create a file.

```bash
touch generate-git-multiple-branches.sh
chmod +x generate-git-multiple-branches.sh
vim generate-git-multiple-branches.sh
```

Then, copy-and-paste the content of the file with lines below.

## Congratulation. You are done with "Git Rebase and Squash" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](8_GitReset_With_Exercise.md)
