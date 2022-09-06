# Let's learn fun git bisect

![image](https://user-images.githubusercontent.com/5396174/187117321-7cb8adce-c4de-4e4f-a2d7-4f207da42b01.png)


Git bisect is an useful built-in tool within git cli that you lets you search a specific commit through binary search. Following shows some situations when git bisect is handy:

- When you found a bug but have no idea when it was introduced
- When a new feature got introduced but have no idea how to trace back
- When there is a performance degrade or improvement but have no idea how to trace back


## How can you get started with git bisect?

1. You start with `git bisect start` to activate git bisect. Now, fun begins!
2. Run `git bisect bad <SHA ID>` where you expect somewhere after a change got introduced
3. Run `git bisect good <SHA ID>` where you expect somewhere before a change got introduced. This **SHA ID** has to happen before a `git bisect bad`. Now, it will start binary search process by splitting a mid point between **bad** and **good**
4. If you did not find a result, you enter `git bisect bad`. This will split in half again and search.
5. If you found a result, enter `git bisect good`
6. Lastly, type `git bisect reset` to terminate `git bisect`


## Congratulation. You are done with "Git Bisect with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](10_ExtraTopic_GitMigrate.md)