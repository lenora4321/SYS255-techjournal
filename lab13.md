# Lab 13 - File Transfer

## Points of interest

### File Transfer Lab Git repository
Most of this lab consisted of generic file transfers using the tools and commands specified in the subsequent sections, and so don't need outlining; however, one section to explain is the creation of and use of the "FileTransferLab git repository.  To see the repository, click [here](https://github.com/lenora4321/FileTransferLab).  Be advised that the content in this repo is not polished or curated.  This repo was created as a go-between for files between a Linux and Windows box.  The git commands found below were used to share data and make changes so that both systems, as well as the repo website, could access the files.

## Technical Terms

### Github and Git
Git is a version-tracking tool that allows for files to be reverted to an earlier state.  Changes can also be delegated to specific branches, and merged with the master branch when ready.  This software is incredibly useful when working with a team, especially on software.  It allows multiple users to edit the same file and later combine them, only changing things that are different between them.  Any collisions between changes to the file are called merge conflicts, and must be sorted out at runtime.  Git was originally created alongside Linux, and is a tool commonly used on the operating system.
Github is a website and storage service that holds remote endpoints for git repositories, while also presenting other features such as comments, pull requests, and issues.  Users must register with the site and can then store code, text, images, or other files.  From here, code can be pushed up, cloned, and edited as normal in with git.

For more information about git, try [this](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/) resource.
*Gowtham Venkatesan, "Learn the Basics of Git in Under 10 Minutes". Free Code Camp, January 5, 2019.*

For more information about GitHub, try [this](https://github.com/about) resource.
*"About".  Github.com, date not provided.*

### File syntax
In a computer file system, several symbols constitute important syntax that are important for the user to be aware of.  SHort descriptions of these are given below.  When run in most terminals, these shorts will be expanded upon.

 - **.** (dot) - signifies the current directory.  This symbol can often replace the destination directory just as a full file address can.
 - **..** (double dot) - signifies the parent directory, or the directory that contains this directory in a tree.
 - **/** (forward slash) - separates files and directories in a file path.  Alone, this symbol can be used to refer to the root directory in some systems.
 - **\\** (bask slash) - separates files and directories in a Windows operating system.
 - **./** (dot slash) - when followed a continuing file name or directory, it refers to starting in the current directory and continuing to a further location from there.

For more information about file paths, try [this](https://automatetheboringstuff.com/chapter8/) resource.
*Al Sweigart, "Automate the Boring Stuff with Python".  No Starch Press, April 4, 2015*

## Commands

```scp``` secure copy.  This command is used to copy files between systems, usually Unix-like systems, but it now works on PowerShell also.  To copy a file, list the source first and then the destination.  To specify a directory on a remote machine, list the IP address or hostname, then the directory, separated by a colon (:).

For examples and more information about the scp command, try [this](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/) resource.
*"How to Use SCP Command to Securely Transfer Files".  Linuxize, May 30, 2020.*

```curl```  "c URL".  A command used to get data from servers, supporting multiple formats such as HTTP, IMAP, POP3, and TELNET.
For more information about curl, try [this](https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/#:~:text=curl%20is%20a%20command%20line,TELNET%2C%20LDAP%20or%20FILE).) resource.
*singhyog "curl command in Linux with Examples".  Geeks for Geeks, May 15, 2019.*

```git add``` Add changes to be staged.  Takes a directory as a parameter.
 - **-a** "All".  Stage all changes in the project, no matter the directory.

```git commit``` Stage the changes into a commit; will be assigned a unique number to be used as an offset from head.
 - **-m** "Message".  Add a message in quotes right after this switch as a tag to go along with it.  Typically includes a short description of the staged changes.

```git push``` Push changes up to repository, typically with a remote.

```git clone``` Clone a git repository from a certain destination, either a directory or a remote origin.

```git pull``` Pull down new changes onto the current branch from the existing directory.

