## Undoing commits

![image](https://user-images.githubusercontent.com/5396174/169838055-e2ac5ba2-dd75-4c89-a13a-dfec0da8ccb6.png)

In this section, we will learn about commands that re-write history and understand when you should or shouldn't use them.

### How Commits Are Made

Every commit in Git is a unique snapshot of the project at that point in time. It contains the following information:

- Pointers to the current objects in the repository
- Commit author and email (from your config settings)
- Commit date and time
- Commit message


Each commit also contains the commit ID of its parent commit.


### Safe Operations

Git's data structure gives it integrity but its distributed nature also requires us to be aware of how certain operations will impact the commits that have already been shared.

If an operation will change a commit ID that has been pushed to the remote (also known as a public commit), we must be careful in choosing the operations to perform.

#### Guidelines for Common Commands

| Command | Cautions |
| ------- | -------- |
| `revert`  | Generally safe since it creates a new commit.|
| `commit --amend` | Only use on local commits.
| `reset` | Only use on local commits.
| `cherry-pick` | Only use on local commits.
| `rebase` | Only use on local commits.

### Reverting a Commit


> **Warning**: Before you reverse the commit, it is a good idea to make sure you will not be inadvertently reversing other changes that were lumped into the same commit. To see what was changed in the commit, use `git show SHA`.

## Congratulation. You are done with "Undoing git commit" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next issue](4_Exercise_Undoing_Git_Commit.md)
