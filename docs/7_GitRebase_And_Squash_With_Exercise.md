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


```bash
#!/bin/bash

FOLDER_GIT=.git
MAIN_JAVA=Main.java
TEST_JAVA=Test.java

if [[ -f $FOLDER_GIT ]]; then
  rm -rf $FOLDER_GIT
fi

if [[ -f $MAIN_JAVA ]]; then
  rm $MAIN_JAVA
fi

if [[ -f $TEST_JAVA ]]; then
  rm $TEST_JAVA
fi

# Making a new git directory
git init

# Creating a new branch called main
git checkout -b main

# main branch - Making a new file called Main.java and commit
touch $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Making a new file called Main.java"

# main branch - Adding a class to Main.java
echo "public class Main {" >> $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Added a class to Main.java"

# Add a new branch - test-branch
git checkout -b test-branch

# test-branch - Create a new file called Test.java and commit

touch $TEST_JAVA

git add $TEST_JAVA && git commit -m "Added a new file called Test.java"

# test-branch - Adding a class to Test.java
echo "public class Test {" >> $TEST_JAVA

git add $TEST_JAVA && git commit -m "Added a class to Test.java"

# test-branch - Adding a main under Test.java
echo "public static void main(String[] args) {}" >> $TEST_JAVA

git add $TEST_JAVA && git commit -m "Added main under Test.java"

# test-branch - Cloasing Test.java
echp "}" >> $TEST_JAVA

git add $TEST_JAVA && git commit -m "Closed Test.java"

# Change branch - main

git checkout main

# main branch - Adding main under Main.java
echo "   public static void main(String[] args) {" >> $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Added main under Main.java"

# main branch - Adding a sample statement
echo "      System.out.println(\"Hello, Git Merge\");" >> $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Added a sample print statement under Main.java"

# main branch - Closing a main function
echo "   }" >> $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Closed main function under Main.java"

# main branch - Closing Main.java
echo "}" >> $MAIN_JAVA

git add $MAIN_JAVA && git commit -m "Closed Main.java"
```

### STEP 3: Execute the script to initialize git structure

Run the following command to execute the script

```bash
./generate-git-multiple-branches.sh
```

Then, run the following command to check few things.

```bash
# Verify that files and directories that got created
ls -la
# Check that two branches got created: main and test-branch
git branch
# Check branches and log
git log --graph --all
```

### STEP 4: Rebase everything with a default option

Now, you should have two branches: `main` and `test-branch`. We want to switch to `test-branch`

```bash
# Check branches
git branch
# Checkout to test-branch
git checkout test-branch
```

Once we checked out to `test-branch`, type the following command to `rebase` what is in `test-branch` to `main`

```bash
git rebase main
```

Now, if we check our branch structure again with:

```bash
git log --all --graph
```

You should see all the commits in `test-branch` got added to the tip of `main` branch.

### STEP 5: Rebase with selective option and git squash

But what if we don't want to bring everything in `test-branch`? And what if we don't like to see all those commit end points but would like to reorganize into one or few commits? In this step, we will explore `interactive` option, which let you select what to do with those commits.

Let's try to reset our file structures and run it again.

```bash
# Delete all Java files
rm *.java
# Delete git reference
rm -rf .git
# Regenerate git structure
./generate-git-multiple-branches.sh
```

Now, if you type `git log --graph --all` again, you should see we are back to where we are first time. Let's type this command:

```bash
# Checkout to test-branch
git checkout test-branch
# Run git rebase in interactive mode
git rebase --interactive main
```

Once you are done, you should see a VI/VIM like editor shown up with three commits that should look something like this.

```bash
pick 1016ffb Added a new file called Test.java
pick 08de73f Added a class to Test.java
pick ac0e74c Added main under Test.java

# Rebase 995c148..ac0e74c onto 995c148 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which 
...
```

If you delete any of line starting with `pick`, then only other commits will be rebased. Other options are interesting, but we will try to use `git squash`. What is **Git Squash**? Git squash is a way to combine multiple commits into one or few commits during a process like git rebase. Let's try to squash 2nd and 3rd commits into first one. Your change should look like this.

```bash
pick 1016ffb Added a new file called Test.java
squash 08de73f Added a class to Test.java
squash ac0e74c Added main under Test.java
```

Once you saved the changes, run `git log --graph --all` to see the change. Notice how 1st, 2nd, and 3rd commit messages are now all shown under one commit message at the top.

## Congratulation. You are done with "Git Rebase and Squash" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](8_GitReset_With_Exercise.md)
