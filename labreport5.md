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
I decided to ask my future replacement: ChatGPT. 
