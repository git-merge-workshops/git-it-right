## Git basic workflows 

Although you can work most changes within GitHub itself, it is highly recommended to get to know how git works by knowing some of most basic git workflow process. There are Git user interface tools for your desktop like GitHub Desktop, Git Kraken, but you can operate everything out from just git CLI. Here are few commands that are essential to know.

```sh
# Pull from the current checked out branch in remote repository
git pull

# change to a branch name that exists
git checkout [branch name] 

# Create a new branch from source branch
git checkout -b [new branch name] [source branch] 

# Check for any change
git status

# Add all files that were modified
git add .

# Add files in selective ways
git add file_name1 file_name2

# Add files to commit with a message
git commit -m "Some commit message"

# Push committed change to GitHub repo
git push
```

This diagram shows how a typical git workflow process will happen

![image](https://media.github.ford.com/user/37856/files/3e84efce-0060-4e1f-be01-b7a1d2356608)

Here, we will walk through how these Git commands from your dev machine are used to interact with GitHub

1. `git clone` to clone the project to your local machine
2. `git add` to addd your changes to the `staging area`
3. `git commit` to take the snapshot of your changes
4. `git push` to upload your changes to GitHub
5. `git fetch` to fetch the latest branches and commits from GitHub
6. `git pull` (a porcelain command of git fetch and git merge) to pull in the latest changes to your branches
7. clone, push, fetch, and pull are the only commands that go over the network

## Our favorite Git command: git status
```sh
$ git status
On branch main
Your branch is up-to-date with 'origin/main'.
nothing to commit, working tree clean
```

`git status` is a command to verify the current state of your repository and the files it contains. Right now, we can see that we are on branch main, everything is up-to-date with origin/main and our working tree is clean.

## Using branches locally

If you type `git branch` you will see a list of local branches.

If you want to see all the branches, including the read-only copies of your remote branches, you can add the --all option or just -a.

```sh
git branch --all
git branch -a
```