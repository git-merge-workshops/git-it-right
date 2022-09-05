## Git Cherry Pick  with Exercise

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

## Congratulation. You are done with "Git Cherry Pick with Exercise" section

![mona](https://user-images.githubusercontent.com/5396174/187010589-a9cbdd9f-f9eb-4e3b-bac0-4abeb8714e8d.png) 

## Let's move to the [next section](7_GitReset_With_Exercise.md)