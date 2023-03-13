# Bash Bugfixing
We will be adding onto lab report 4 and fixing bugs as fast as possible, but this time we'll do it in a bash script. For simplicity, we will not be including SSHing into another computer in the bash script. 

## The Foundation
In lab 4, after SSHing, we performed the following steps to fix the bug:

1. `git clone git@github.com:slayyden/lab7.git`
2. `cd lab7`
3. `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`
4. `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`
5. `vim ListExamples.java`
6. Enter the keystrokes: `42jwwi<backspace><backspace>2<esc>:wq` to fix the bug. 
7. `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`
8. `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`
9. `git add ListExamples.java`
10. `git commit -m "fixed bug"`
11. `git push`

Most of what we have can be performed in a bash script, but steps 6 and 7 cannot. We need to edit the file without vim or some other command line editor. I don't know how to do that but I think I know someone who does.

## Oh Great ChatGPT, How Do I Edit A File From the Command Line?
I decided to ask my future replacement: ChatGPT. Here's what it had to say:
<img width="557" alt="image" src="https://user-images.githubusercontent.com/26509702/224586647-bc723493-459f-4010-806f-7dee6946a883.png">

Replacing steps 6 and 7 with the command ChatGPT gave us, we can now put everything in a bash script. 

```console
git clone git@github.com:slayyden/lab7.git
cd lab7
 
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

sed -i '43s/.*/        index2++/' ListExamples.java

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
git add ListExamples.java
git commit -m "fixed bug"
git push
```

Let's run it.

<img width="670" alt="image" src="https://user-images.githubusercontent.com/26509702/224587095-8acedc6c-3c37-40eb-a115-2d6b809448a5.png">

Looks like we forgot to tell ChatGPT to add a semicolon. Let's fix that.

<img width="513" alt="image" src="https://user-images.githubusercontent.com/26509702/224587190-5931d89b-7338-4084-b43f-47db4d81798a.png">

Let's edit the script and run it again.

## The Final Script
Seems like we need to delete the repo folder each time we run the script.
<img width="803" alt="image" src="https://user-images.githubusercontent.com/26509702/224587374-e07cb16d-6f58-4a56-8503-d0c570048a79.png">

After adding that functionality to the bash script, it now looks like this:

```console
rm -rf lab7
git clone git@github.com:slayyden/lab7.git
cd lab7

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

sed -i '43s/.*/        index2++;/' ListExamples.java

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
git add ListExamples.java
git commit -m "fixed bug"
git push
```

Hopefully it works this time.

<img width="694" alt="image" src="https://user-images.githubusercontent.com/26509702/224587676-35e4c262-33d3-4113-a99d-1847e6fdcbcd.png">

Seems like it did! The commit shows up on github.

<img width="834" alt="image" src="https://user-images.githubusercontent.com/26509702/224587716-5a654e36-40c7-43cc-951e-a4626a22595a.png">

## How Fast is it?
By using the `time` command, we can see that the bugfixing takes a total of 4.319 seconds, which is much faster than any human attempt I am aware of!

<img width="138" alt="image" src="https://user-images.githubusercontent.com/26509702/224587867-2843213c-4a1a-4248-bc1c-7d1f93a52033.png">

