# Git Commit Amend with Exercise

In last section, you learned about a simplest posible way to undo a commit: `git revert`. In this section, you will learn about `git commit --amend`, which is a way to modify a previous commit in a case you want to change what already had happened. 

`git commit --amend` allows us to make changes to the commit that **HEAD** is currently pointing to. Two of the most common uses are:

- Re-writing commit messages
- Adding files to the commit

## Exercise - Git Commit Amend

We will go through a simple exercise to try to out `git commit --amend`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: You can continue to use a same directory and a same script for other continuing exercises. However, the idea is to allow users to pick up from any step that they want to review later without depending on other steps. In addition, it is always easy to work with a clean slate. Because of this, you will see same or similar commands and instructions getting copied over multiple time.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitCommitAmendDemo`
mkdir GitCommitAmendDemo
# Go inside the directory
cd GitCommitAmendDemo
```

### STEP 2: Create a new file to initialize git structure

> NOTE: Again, you can continue using this same file for other exercises. It is up to you how you want to manage this.

Create a new file called `generate-git-single-branch.sh`. You can do it with either by going inside a directory and create a file through a tool like **Visual Studio Code**. Or, you can use a tool like **VIM** to quickly create a file.

```bash
touch generate-git-single-branch.sh
chmod +x generate-git-single-branch.sh
vim generate-git-single-branch.sh
```

Then, copy-and-paste the content of the file with lines below.

```bash
#!/bin/bash

FOLDER_GIT=.git
README_FILE=README.md

# Making a new git directory
git init

# Creating a new branch called main
git checkout -b main

# main branch - Making a new file called README.md and commit
touch $README_FILE

git add $README_FILE && git commit -m "Making a new file called README.md"

# main branch - Adding a class to Main.java
echo "# Trying out Git Revert" >> $README_FILE

git add $README_FILE && git commit -m "Added a header to README.md"

# main branch - Adding some description
echo "" >> $README_FILE
echo "Welcome to Git Merge! Here, we will try out git revert exercise" >> $README_FILE
echo "" >> $README_FILE

git add $README_FILE && git commit -m "Adding some description"

# main branch - Adding some more description
echo "" >> $README_FILE
echo "**Git Merge** conference is going to be awesome." >> $README_FILE
echo "" >> $README_FILE

git add $README_FILE && git commit -m "Adding some more description"
```

### STEP 3: Execute the script to initialize git structure

Run the following command to execute the script

```bash
./generate-git-single-branch.sh
```

Then, run the following command to check a new file called `README.md` and a `.git` directory got created.

```bash
ls -la
```

### STEP 4: Introduce a new commit with a purposedly intended error

Check the content of README.md. Next, we will purposedly make a commit with a typo with a following line change. Open up your `README.md` and add this line at the end of the file then save.

> **git reset** is the best way to make a change to an existing commit without rewriting history

And then you can run the following command to make a commit.

```bash
git add README.md && git commit -m "Purposedly making a typo"
```

### STEP 5: Amend the previously wrong commit with git amend

Obviously, you know it is not **git reset** that is the correct answer. So, we want to change that word to **git revert**. Run `git log` command to verify our last commit id. You may want to take a screenshot just to compare later. Then, modify your `README.md` file and fix the wording from `git reset` to `git revert`. Then, run the following commands in sequence.

```bash
# Add to staging
git add README.md
# git commit --amend -m "Adding an explanation about git revert"
```

If you run that, you can check the status by running these commands.

```bash
# Check your file content with
cat README.md
# Check your commit log
git log
```

In your git log, you should notice that there are still same number of git commits, but your last commit should be replaced with a new one with a new message.

## Congratulation. You are done with "Git Commit Amend with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](6_GitCherryPick_With_Exercise.md)