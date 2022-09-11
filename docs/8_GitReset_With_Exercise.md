# Git Reset with Exercise

**Git reset** is the command that we want to use when we want to move the repository back to a previous commit, throwing all changes made after that specific commit. Git reset comes in three forms: `soft`, `mixed`, and `hard`. By default, if you don't specify anything, it is `mixed`.

![image](https://user-images.githubusercontent.com/5396174/189043666-d29cd802-e256-4aad-a7a5-d96e9a2e3624.png)

To properly understand different modes of how `git reset` works, it is essential to know git's three ways to store states: `working directory`, `staging`, and `commit history`. 

1. **Working Directory**: By default, when you create, delete, or modify files, that will go into working directory stage
2. **Staging**: Then, when you do `git add` those changed files, that will go to staging stage.
3. **Commit history**: Lastly, whne you do `git commit`, those files in `staging` will go to git commit history.

Now, combining those ideas, here are how different modes of `git reset` differ:
- `git reset --soft` can revert back what happened in commit history but don't touch what is in **working directory** or **staging**
- `git reset --mixed` or `git reset` can revert back what is in staging and commit history, but does not change files that were modified
- `git reset --hard` basically revert back everything including files that are changed.

![image](https://user-images.githubusercontent.com/5396174/189043752-871dc855-1cae-4879-a86a-e66f54687e7e.png)


And you can see, `git reset --hard` is the most dangerous operation, so use it very sparingly.

## Exercise - Git Reset

We will go through an exercise to try to out `git reset`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: You can continue to use a same directory and a same script for other continuing exercises. However, the idea is to allow users to pick up from any step that they want to review later without depending on other steps. In addition, it is always easy to work with a clean slate. Because of this, you will see same or similar commands and instructions getting copied over multiple time.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitResetDemo`
mkdir GitResetDemo
# Go inside the directory
cd GitResetDemo
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

### STEP 4: Git reset with soft option

We will first try to reset our change with `--soft` option. This is the safest operaiton as it will just revert commits. Run the following command to check commit history.

```bash
git log --graph --all
```

Copy the commit id right below the top most one. It should say `Closed main function under Main.java` as its commit message. Then, type in the following command.

```bash
git reset --soft <SHA ID you copied from>
```

Run `git log --graph --all` again. You should see that top most commit got removed. However, if you check your file with the following two commands, you should see that `Main.java` is not in staged state while its content is unaffected.

```bash
# Check status of git state
git status
# Check content of Main.java
```

### STEP 5: Git reset with default option, which is mixed

Let's now try to run with `--mixed` option, which is also default `git reset` option. Before that, type `git log --graph --all` again to see git history. Again, copy commit id right below the top most one. It should say with a commit message `Added a sample print statement under Main.java`. Then, type in the following command.

```bash
git reset <SHA ID you copied from> 
```

or `git reset --soft <SHA ID you copied from>`

You should see a following message.

```bash
Unstaged changes after reset:
M	Main.java
```

Check your file status with few commands.

```bash
# Check that commit id is gone
git log --graph --all
# Check that Main.java file is now unstaged
git status
# Check that file content did not get affected
cat Main.java
```

### STEP 5: Git reset with hard option

Now, we are going to do most destructive operation: `git reset --hard`. Use this with a high caution because it can remove all changes you made. Again, run `git log --graph --all` again to see your git history. Since this is a last exercise, you can technically pick anything other than top most one. But if you followed a same approach, you will pick one with a commit message `Added main under Main.java`. Copy its git commit id. Then, run the following command.

```bash
git reset --hard <<SHA ID you copied from>
```

Then, you will see a message like this.

```bash
HEAD is now at 9a1ab03 Added main under Main.java
```

Check few things again like last time.

```bash
# Check that commit id is gone
git log --graph --all
# Check that Main.java file is now unstaged
git status
# Check that file content got changed!
cat Main.java
```

Main difference about this command is that it actually modifed your file contents. Because of this, you should exactly know what you are doing with `git hard --reset` option.

## Congratulation. You are done with "Git Reset with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](9_GitBisect_With_Exercise.md)
