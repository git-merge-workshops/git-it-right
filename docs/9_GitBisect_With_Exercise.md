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

## Exercise - Git Bisect

We will go through an exercise to try to out `git bisect`. As long as you have **Git CLI** installed in your computer, you don't need the internet connection.

> NOTE: For this exercise, you have to use two different scripts, which is unique for this exercise only.

### STEP 1: Create a directory and cd into it

This will depend on your operating system. 

- **Mac OS/Linux**: Open up a Terminal window/shell window and make sure you are in a right directory (e.g. `pwd`). 
- **Windows**: Open up **Git CLI** by clicking on bottom left Windows button and search for **Git CLI**. Make sure you are in a right directory. 

Instructions after that should be same. 

```bash
# Create a directory called `GitBisectDemo`
mkdir GitBisectDemo
# Go inside the directory
cd GitBisectDemo
```

### STEP 2: Create a first file to generate git structure

Create a new file called `pre-generate-git-bisect.sh`. You can do it with either by going inside a directory and create a file through a tool like **Visual Studio Code**. Or, you can use a tool like **VIM** to quickly create a file.

```bash
#!/bin/bash

FILE=book-harry-potter.md

# Making a new git directory
git init

# Creating a new branch called main
git checkout -b main

if [[ -f "$FILE" ]]; then
  rm $FILE
fi

touch $FILE

echo "# Harry Potter and the Sorcerer's Stone" >> $FILE

git add $FILE && git commit -m "Title"

echo "![Harry Potter cover](./cover_book.jpg)" >> $FILE

git add $FILE && git commit -m "Cover picture"

echo "After murdering Harry's parents, James and Lily Potter, evil Lord Voldemort puts a killing curse on Harry, then just a baby" >> $FILE

git add $FILE && git commit -m "Add first description"

echo "The curse inexplicably reverses, defeating Voldemort and searing a lightning-bolt scar in the middle of the infant's forehead." >> $FILE

git add $FILE && git commit -m "Add second sentence"

echo "Harry is then left at the doorstep of his boring but brutish aunt and uncle, the Dursleys." >> $FILE

git add $FILE && git commit -m "Add third sentence"

echo "For 10 years, Harry lives in the cupboard under the stairs and is subjected to cruel mistreatment by Aunt Petunia, Uncle Vernon and their son Dudley." >> $FILE

git add $FILE && git commit -m "Add fourth sentence"

echo "On his 11th birthday, Harry receives a letter inviting him to study magic at the Hogwarts School of Witchcraft and Wizardry." >> $FILE

git add $FILE && git commit -m "Add fifth sentence"

echo "Harry discovers that not only is he a wizard, but he is a famous one." >> $FILE

git add $FILE && git commit -m "Add sixth sentence"

echo "He meets two best friends, Ron Weasley and Hermione Granger, and makes his first enemy, Draco Malfoy." >> $FILE

git add $FILE && git commit -m "Add seventh sentence"
```

This should have initialized a basic git structure and created a new file called `book-harry-potter.md`. You can check with the following commands.

```bash
# Check files to check .git and book-harry-potter.md
ls -la
# Check git commit history
git log --graph --all
```

### STEP 3: Intentionally introduce a malicious change

Next, we are intentionally going to create a bad commit. Modify your `book-harry-potter.md` and add the following sentence at the end: `Harry meets Darth Vader, and he finds out that he is a lost son of Darth.`

Then, use this command to make a commit.

```bash
git add book-harry-potter.md
git commit -m "Adding some malicious change"
```

> In this example, we made it really obvious what is a bad change. However, in real world, it will be not so obvious.

### STEP 4: Run the second script generate remaining commits

Create a second file called `post-generate-git-bisect.sh`. You can do it with either by going inside a directory and create a file through a tool like **Visual Studio Code**. Or, you can use a tool like **VIM** to quickly create a file.

```bash
#!/bin/bash

FILE=book-harry-potter.md

echo "At Hogwarts the three friends are all placed into the Gryffindor house. Harry has a knack for the school sport, Quidditch, and is recruited onto the Gryffindor team as its star Seeker." >> $FILE

git add $FILE && git commit -m "Add eighth sentence"

echo "Perusing the restricted section in the library, Harry discovers that the Sorcerer's Stone produces the Elixir of Life, which gives its drinker the gift of immortality" >> $FILE

git add $FILE && git commit -m "Add ninth sentence"

echo "After realizing that Voldemort might be after the stone, Albus Dumbledore had it moved it to Hogwarts for safekeeping." >> $FILE

git add $FILE && git commit -m "Add tenth sentence"

echo "Harry finds out that when she died, Lily Potter transferred to her son an ancient magical protection from Voldemort's lethal spell" >> $FILE

git add $FILE && git commit -m "Add eleventh sentence"

echo "This protection is what allowed Harry as an infant to survive Voldemort's attack. It also helps Harry keep Voldemort from possessing the Stone, which Dumbledore agrees to destroy." >> $FILE

git add $FILE && git commit -m "Add twelveth sentence"
```

Then, execute the file with `./post-generate-git-bisect.sh` command.

Check, your commit status.

```bash
# Check git commit history
git log --graph --all
# Check content of updated book-harry-potter.md
cat book-harry-potter.md
```

We now have everything ready to run our git bisect search.

### STEP 5: Search a bad commit through git bisect

To start, run the following command.

```bash
git bisect start
```

This will trigger git bisect mode, which will split our git log into two do binary search. Next, we need to mark two commits: a bad commit and a good commit. To mark a good commit, you need to find out where you believe a commit id that did not have a malicious commit. For us, we will mark the very first commit. It should say with a message `Title`

```bash
# Mark a good commit
git bisect good <Last know good commit SHA ID>
```

This should print out  amessage like 

```bash
Bisecting: 6 revisions left to test after this (roughly 3 steps)
[be88cc1c090ab114bdd79193256fc29f01d1ebe5] Add sixth sentence
```

Next, we need to mark a bad commit. Let's pick the very top one.

```bash
# Mark a bad commit
git bisect bad <Last known bad commit SHA ID>
```

This should print a message like the following.

```bash
Bisecting: 6 revisions left to test after this (roughly 3 steps)
[be88cc1c090ab114bdd79193256fc29f01d1ebe5] Add sixth sentence
```

Let's check our file `book-harry-potter.md` file by opening with either `cat book-harry-potter.md` or a text editor. You should not see an error. So, we will type `git bisect good`.

You should see a message like this, and we did not yet find the culprit.

```bash
Bisecting: 3 revisions left to test after this (roughly 2 steps)
[cf4333d93020d4a33dbd1751dee8de3ce50cea8c] Adding some harry potter book change
```

Now, if you open `book-harry-potter.md` to see its content, you should see it has a malicious commit. Type `git bisect bad` this time. You should then see a message like this.

```bash
Bisecting: 0 revisions left to test after this (roughly 1 step)
[7df8ad9dfa2d657e6c309974af900eebc77492f2] Adding some malicious change
```

Aha! This is where a bad commit happens. We can check our content of `book-harry-potter.md` as well. 

We can then modify our file `book-harry-potter.md` to either fix it or remove the line, but we will do in next step. For now, copy the commit id where you discover that malicious change.

Get out from git bisect mode by typing the following command.

```bash
git bisect reset
```

### STEP 6: Fix the change

There should be a number of different ways to fix the problematic line, but we will try to delete that line. Modify your  `book-harry-potter.md` to remove the line. Then, type the following command.

```bash
git add book-harry-potter.md
git commit -m "Removing that malicious change"
```

Now, your file is fixed!

## Congratulation. You are done with "Git Bisect with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](10_WrappingUp.md)