# Git Revert with Exercise

![image](https://user-images.githubusercontent.com/5396174/188518491-665fffac-b863-4e2d-bde0-36f727f62c5f.png)

Among different ways to undo our previous git commits, `git revert` is the safest way to do so. `git revert` does not actually overwrite the existing commit. Instead, `git revert` understands how to invert the changes introduced by the commit and appends a new commit with the inverted content. This operation is safe because it prevents git from losing git history.

## Exercise - Git Revert

We will go through a simple exercise to try to out `git revert`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: You can continue to use a same directory and a same script for other continuing exercises. However, the idea is to allow users to pick up from any step that they want to review later without depending on other steps. In addition, it is always easy to work with a clean slate. Because of this, you will see same or similar commands and instructions getting copied over multiple time.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitRevertDemo`
mkdir GitRevertDemo
# Go inside the directory
cd GitRevertDemo
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

### STEP 4: Introduce a new change and revert back

Check the content of README.md. Try to add one new line change to `README.md` file. Then, run the following command to commit.

```bash
git add README.md && git commit -m "Adding a new change"
```

If you type the following command, you should see the history of git.

```bash
git log --graph --all
```

Copy the top most commit SHA id. Then, you can type the following command to revert back to the last commit.

```bash
git revert <Copied SHA ID>
```

You can check the status by typing `git log --graph --all` and the content of `README.md` file again. Notice that your previously copied commit is still there, but there is a new commit that just reverts back your file change.

### STEP 5: Little more interesting exercise...

What will happen if you want to revert back to a previous point after some changes are already made? Let's test it out! Make few more commits like last one. But in this time, don't pick the very last commit id but a commit that happened little before. What happens now?

## Congratulation. You are done with "Git Revert with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](5_GitCommitAmend_With_Exercise.md)
