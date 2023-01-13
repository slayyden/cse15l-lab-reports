# Lab 1: Remote Access
Remote access is often a necessary when you need to perform a task using a computer that you cannot be physically in front of. This post will detail the basics of performing such a maneuver using course-specific accounts at UCSD from a Mac.
## Part 1: Installing Visual Studio Code
Every CSE class at UCSD seems to use Visual Studio Code (VSCode), so we will be using that for this tutorial. In this first section, we will go over installing it. If you already have it, skip the part 2.

First, we will download VSCode [here](https://code.visualstudio.com/Download). The page should look something like this:
<img width="984" alt="image" src="https://user-images.githubusercontent.com/26509702/212185456-f1b0602a-d96b-478a-aa83-4528ed8b6047.png">
Download a .zip file and select Intel or Apple Silicon depending on your system.

Then, you want to:
* Double click on the file in your Downloads folder to unzip it.
* Drag the application into the applications folder.

You should now be able to launch VSCode from your applications folder. The application will open and greet you with a home screen similar to this:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26509702/212186113-b6d92585-8aa5-4ffb-b608-f69b0156b01d.png">

## Part 2: Remotely Connecting
### Part 2a: Obtaining Login Info
Each UCSD class will have its own remote login info. To find it, visit [this link](https://sdacs.ucsd.edu/~icc/index.php). 
<img width="1261" alt="image" src="https://user-images.githubusercontent.com/26509702/212186958-0b189f8c-3022-4ddc-846d-2c835ade1f83.png">
Under "Forgot Username or New Student?" enter your last name and PID. This should show you an account name specific to your class. It will likely have the class name in it. For example, every account for CSE 15L in Winter 2023 starts with "cse15Lwi23". **You must reset your password for the account before you can use it.** Details for doing so are in [this document](https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit).
### Part 2b: Logging In
Open a terminal by going to the top bar and clicking Terminal -> New Terminal. You can connect remotely by typing 
```
$ ssh ___________@ieng6.ucsd.edu 
```
Fill in the blank with your username.
