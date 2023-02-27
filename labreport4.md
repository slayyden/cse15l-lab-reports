# Bugfixing Speedrun!
We will complete the following steps as fast as possible:
1. Log into ieng6
2. Clone your fork of the repository from your Github account
3. Run the tests, demonstrating that they fail
4. Edit the code file to fix the failing test
5. Run the tests, demonstrating that they now succeed
6. Commit and push the resulting change to your Github account (you can pick any commit message!)

For each step in this list, there exists at least one screenshot documenting it. However, multiple steps may share the same screenshot as they are part of the same command. These steps are crafted not to be practical but to maximize speed. As a result, the full optimizations will only work on your second run through of the instructions. You should be able to complete all the steps after step 3 in under 30 seconds.

## 1. Log into ieng6
If this is your first run, type into your terminal `ssh cs15lwi23___@ieng6.ucsd.edu`, replacing the underscores with the letters associated with your account. Then press `<enter>`. 

If this is not your first run, the `ssh` command should be the most recent one, so simply press `<up><enter>`.

<img width="578" alt="image" src="https://user-images.githubusercontent.com/26509702/221699200-2fec4b8c-db36-4ab0-a134-bed83d6e483a.png">

## 2. Clone your fork of the repository. 
Now you are in the ieng6 machine. If this is your first run, go back to the github page in your web browser to copy the ssh url for your fork. Then, type the command `git clone git@github.com:slayyden/lab7.git; cd lab7`, replacing my ssh url with the url for your fork and then press `<enter>`. 

If this is not your first run, type `<ctrl>r` to search through your history and then `git<space>cl<enter>`.

<img width="914" alt="image" src="https://user-images.githubusercontent.com/26509702/221700026-3b258301-4495-4da2-a709-2fab5f99158f.png">

This should clone the repo and make your working directory the root directory of the cloned repository.

## 3. Run The Tests, Demonstrating That They Fail
If this is your first run, type `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java;java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` and then press `enter`.

If this is not your first run, press `<up><up><up><up><up><enter>` to get the same command from the previous run through. 

<img width="1038" alt="image" src="https://user-images.githubusercontent.com/26509702/221701020-e9766fcf-b7e6-47a3-b63a-1eb79304f65f.png">


## 4. Edit the code to fix the bug
If this is your first run, type `vim ListExamples.java`.

If this isn't your first run then type `<ctrl>r` followed by `vi` and then `enter` to get the same command from the previous run.

In vim, perform the following keystrokes `42jwwi<backspace><backspace>2<esc>:wq` to fix the bug. The file should look something like this once you're done:

<img width="468" alt="image" src="https://user-images.githubusercontent.com/26509702/221701679-b560a429-d936-4233-a9d7-994e09aa24d9.png">

## 5 and 6 Run the Tests and Push the Changes
If this is your first run, type `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java;java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests;git add ListExamples.java;git commit -m "fixed bug";git push` and then `enter`. This will compile the java files, run the JUnit tests, add the modified file to your commit, create the commit, and then push the changes. Copy the command to your clipboard to use in future runs.

If this isn't your first run, paste the command with `<cmd><v>` on a MacOS client or `<ctrl><v>` on a Windows client. Then, press `enter` to run the command. You are done.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26509702/221702234-b8a74aa2-3302-4653-a7ad-cf2425fe6f5e.png">
