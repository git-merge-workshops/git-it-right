# Learn different ways to undo or to change git commits

![back2thefuture](https://user-images.githubusercontent.com/5396174/188551977-be6e5031-6e67-4d3a-b411-b0fb23dd4b0a.jpg)

In this section and following sections, we will learn about different git commands that re-write history and understand when you should or shouldn't use them.

## How Commits Are Made

Every commit in Git is a unique snapshot of the project at that point in time. It contains the following information:

- Pointers to the current objects in the repository
- Commit author and email (from your config settings)
- Commit date and time
- Commit message

Each commit also contains the commit ID of its parent commit.

## Safe Operations

Git's data structure gives it integrity but its distributed nature also requires us to be aware of how certain operations will impact the commits that have already been shared.

If an operation will change a commit ID that has been pushed to the remote (also known as a public commit), we must be careful in choosing the operations to perform.

### Guidelines for Common Commands

| Command | What it is |
| ------- | -------- |
| `revert`  | Instead of removing an existing commit, it inverts the change by creating a new commit |
| `commit --amend` | Convenient way to modify the most recent commit by combinig changes with the previous commit |
| `cherry-pick` | Pick a commit from one branch and apply on another branch |
| `rebase` and `squash` | Integrate changes from one branch to another |
| `reset` | Reset your current head to a specified state |

In our next sections, we will go each topic in more deteail and learn by doing prepared exercises.

> **Warning**: Before you reverse the commit, it is a good idea to make sure you will not be inadvertently reversing other changes that were lumped into the same commit. To see what was changed in the commit, use `git show SHA`.

## Congratulation. You are done with "Undoing git commit" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](4_GitRevert_With_Exercise.md)
