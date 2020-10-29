# Lab 9 - Bash Scripting

## Points of interest

### Running a shell file
To run a newly created shell (.sh) file in bash, it needs to be given executable permissions and called from a location where it knows to run it, assuming that the file is not in a directory already contained in $PATH.  Below is a simple set of commands used to allow a shell script t be run out of the current directory, assuming that that directory is the same directory where the file is found.

 1. ```chmod +x filename.sh```
 2. ```./filename.sh```

Alternative to running command number 2, the user could also add the directory to $PATH so that the system can find it on its own when it is evoked from anywhere, or the user could invoke ```bash filename.sh``` to call the script similar to how it is called above.
 
### Script creation
To create a script in bash, simply use 	```touch``` to create a file with the extension .sh, and then use any test editor, such as nano or vim, to edit it.  Start the script with ```#!/bin/bash```, and then begin typing commands to run when the script is evoked as a command itself.  Below are some details to implementing certain features of programming into a script.

#### Basic for loops
For loops are a common find in many high-level programming and scripting languages such as C++ and JavaScript.  They typically work by using the keyword "for" and declaring a variable, what conditions to continue under, and how the variable increments (or decrements) each time the loop goes around.  The code within it is then repeated each time the conditions to continue are met.

In bash, there are several ways to make a for loop, but the most common way is by using the embedded command ```seq``` to determine how long the loop goes for.  This command can take up to 4 parameters, though typically only takes 2: the start of value and the end value.  The third parameter, placed in the middle, is used to determine how the variable increments as the loop goes around.  Two simple examples of a for loop using seq are shown below.  Note that the portions shown below are only the first line, which would normally be followed by body code and then the keyword ```done``` to signify where the loop ends.

 - ```for i in $(seq 1 10); do``` start a variable $i at the value 1 and continue until it reaches 10.  Since no increment is specified, 1 is implied.
 - ```for i in $(seq 10 -2 1); do``` start a variable $i at the value 10 and continue until it reaches 1, decrementing by 2 each time.

In combination with the loop structure and the seq command, we can implement a for loop in bash by simply putting the code that we want to repeat inside of the ```do```...```done``` code.  Node that a loop will also work as a for...each loop if given an iterable, but that is beyond the scope of this entry.

#### I/O
Input/Ouput, or "I/O", can be achieved in a bash script by using the command ```read```.  This, combined with the -p option and a string to output, will prompt the user for an input with the given string and then save it to a variable specified in the command.  Examples of this are given below.

 - ```read -p "Enter a number", a``` the input is saved here into the variable $a
 - ```read -p "Please write the name of your first pet, pet``` the input here is saved into the variable $pet

This can be used in a bash script to retrieve user data dynamically and in a more user-friendly way when running a program.

#### Parameters
Parameters, also called arguments, are pieces of data passed to a function or command when it is called to be used in the function's implementation.  A good example of a parameter would be the two values to be added in a sum function.  In bash, arguments are provided by writing the values or variables to be passed right after the command and any attached options, typically space delimited.

To access these variables in the bash script, the dollar sign, "$", and the number referring to the parameter order or parameters is then used.  In other words, if the program ```sum``` is called as dictated below, ```$1``` would refer to the first parameter, 7, and ```$2``` would refer to the second parameter, 2.

```sum 7 2```

In a function that may have a variable number of parameters, use the built-in variable $# to grab the number of parameters given, so that there is not an access violation trying to refer to a parameter that was not given.

## Technical Terms

### Piplining ( | )
Piplining, or piping, is a technique used in bash scripting in order to direct the output of one command to another command.  This happens typically on one line, with a pair of commands separated by the pipe character, " | ", with the first command to the left of the pipe and the second to the right.  Piped commands can also be chained together, with each new layer added on to the right of the last pipe.

A simple example of this would be the combination of the ```ls``` and the ```grep``` commands.  Say for example you want search the output of all the files ans subdirectories within the directory "school-work" for the term "lab".  You would first type the ls, the directory to search, and then the pipe character, " | ", and the grep command with the parameter "lab".  This would take everything that would be shown in ls and pass it the grep as input, and grep would return only those files with the term "lab" in them.  This example is shown in the line of code below.

```ls /school-work | grep "lab"```

### Bash and bash scripting
Bash, which stands for "Bourne Again SHell", is the default shell on most Linux systems.  A shell is a piece of software that is used to take in commands and hand them off to the operating system for their execution.  It may perform things like regex matching and expansion before anding it off, as well as the calling of certain environmental variables.  Bash scripting is simply the combining of multiple commands in such a way that they can be called to achieve a narrow goal, such as finding the number of files that fit a certain regular expression or adding a number of users with particular usernames to the /etc/passwd file.  This is typically done in such a way that it can be repeated many ties with different criteria and produce a result.  As such, a bash script is usually stored in a file with the ending .sh and given the execute (x) permission, so that it can be called over and over.

For more information about bash, try [this](https://linuxcommand.org/lc3_lts0010.php) resource.
*Shotts, William E., Jr., "What is 'the shell'?"  linuxcommand.org, date not provided.*

## Commands

```env``` "Environment variables".  This command will output all current environment variables that the shell has access to.  Environment variables are pieces of data often used by commands throughout a shell in order to render output in with respect to certain parameters.  This command will often print out things like ```$PATH```, ```$HOSTNAME```, and many color codes used to make reading more user-friendly.

```$PATH``` The list of directories searched for executable files when a command is run, in order from left to right.  Colon delimited.

```$HISTSIZE``` The size of the data kept for history of commands.  This number usually stands for the number of past commands retrievable in a shell, specifically by commands like ```history```.

```bash``` Command used to execute shell scripts and commands in the Bourne Again SHell.  Can be given the name of an executable file to run and will run it.

```touch``` Command used to create a new file in a directory.  Example: ```touch filename.txt```.

```awk``` Command used to separate output into variables that can be formatted as the user sees fit.  This command can take a delimiter as an argument, so that the output given to it can be divided up upon that character and used to selectively display the data elements afterward.  Often used in conjunction with the term "print" to sprint out characters and fields as output.

 - **-F** Field separator.  Specify a character used to delimit the input into individual fields.

```mkdir``` Make directory.  Command used to create a new directory.  Example: ```mkdir directory-name```.

```grep``` Command use to search input for a certain term (or regular expression if used in extended mode or in other versions such as egrep) and return only the lines of output that match the requested search term.  Example: ```grep "lab" filetosearch.txt```.

 - **-v** Inversion of grep command--show only those lines that do not contain the specificed search term.

```nmap``` Network map.  Command used to scan ports and network for various relevant elements such as port number and type, port activity, connections, and operating systems of connected devices.  

For more information on how to use nmap, try [this](https://nmap.org/book/man.html) resource.
*Lyon, Gordon, "Chapter 15. Nmap Reference Guide".  Date not provided.*


