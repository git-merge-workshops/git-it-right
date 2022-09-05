## Git Revert with Exercise

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
echo "**Git Merge** confernece is going to be awesome." >> $README_FILE
echo "" >> $README_FILE

git add $README_FILE && git commit -m "Adding some more description"
```

## Congratulation. You are done with "Git Revert with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](5_GitCommitAmend_With_Exercise.md)