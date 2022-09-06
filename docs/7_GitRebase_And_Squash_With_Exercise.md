# Git Rebase with Squash

`git rebase` enables you to modify your commit history in a variety of ways. For example, you can use it to reorder commits, edit them, squash multiple commits into one, and much more.

To enable all of this, rebase comes in several forms. In this section, we will explore basic rebase, rebase with interactive option, and rebase with squash.

Why would you want to use `git rebase`? The goal of rebase is similar to that of `git merge`: they are both trying to integrate one branch to another. Now, if you are using web based git platforms like GitHub, GitLab, or BitBucket, you are maybe familiar with the concept of **Pull Requests** or **Merge Requests**. `git merge` or `git rebase` provides a similar way to merge one branch with another but through a plain simple git way. 

Merge works by creating a new commit in a destination branch by tying together the histories of both branches, and it is a safe operation. 

Rebase, in other hand, moves the entire commits, though there is a selective way to choose, to the tip of destination branch. This essentially re-writes the project history.

## Congratulation. You are done with "Git Rebase and Squash" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](8_GitReset_With_Exercise.md)