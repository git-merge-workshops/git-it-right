# Git Cherry Pick  with Exercise

**Cherry picking** allows you to pick up a commit from your reflog or another branch of your project and move it to your current branch. It is a very powerful command that allows a specific git commit from a reference and append to the current working HEAD.

When will it be helpful to use cherry pick? Cherry pick can be useful for following scenarios:
- You or somebody else accidentally made a commit to a wrong branch
- Your team needs that specific change, whether it is a new feature or a fix, made by somebody else

## Exercise - Git Commit Amend

We will go through an exercise to try to out `git cherry-pick`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: You can continue to use a same directory and a same script for other continuing exercises. However, the idea is to allow users to pick up from any step that they want to review later without depending on other steps. In addition, it is always easy to work with a clean slate. Because of this, you will see same or similar commands and instructions getting copied over multiple time.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitCherryPickDemo`
mkdir GitCherryPickDemo
# Go inside the directory
cd GitCherryPickDemo
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

### STEP 4: Cherry pick a branch from test-branch

First, let's check the contents are different between `main` branch and `test-branch` branch. 

```bash
# See the files in current main branch and verify the contents
ls
cat Main.java
# Change to test-branch
git checkout test-branch
# See the files in current test-branch and verify the contents
ls
cat Main.java
cat Test.java
```

Run the following command to find out the last commit id from `test-branch` and copy the git commit id.

```bash
# See all logs in all branches
git log --graph --all
```

Switch to `main` branch again and cherry pick the last commit from `test-branch`

```bash
# Switch to main branch
git checkout main
# Cherry pick a branch
git cherry-pick <Last SHA ID from test-branch>
```

Check the content from main branch. You should see the chages made for `Main.java` file and a new `Test.java` file. You can also verify that a new commit got created on your `main` branch.

```bash
git log --graph --all
```

What will happen if you picked a branch from earlier point? This will result in a conflict that you need to resolve. Try it and see!

## Congratulation. You are done with "Git Cherry Pick with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](7_GitRebase_And_Squash_With_Exercise.md)