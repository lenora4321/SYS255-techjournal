# Lab 3 - DHCP Linux Box Setup

## Points of interest

### Cabling re-cap

### nmtui Network Setup

## Technical Terms

### SSH

### DHCP

## Linux

## Commands

### nmtui 

### adduser <name>
"Add user".  Create a new user of the given name.  User will be added to a group of their own name, but no other groups.

### passwd <name>
"Password".  Change the password for a given username.  If there is already a password set, it will likely ask for the old password.  Will require password to be retyped for certainty.

### systemctl restart network

### usermod <groupname> <username>
"User Modify".  Add the given user to the given group.  In CentOS, the admin user is called "wheel".

**-a** Append, an option used to add the new user to the group, else will attempt to remove that user from the group

**-G** Option that allows for multiple groups, separated by commas.

### cd <directory>
"Change Directory".  Similar to a folder in other operating systems, a directory is a container for other files.  Some common directories in Linux are /etc, /dev, and /home.  This command allows you to shift between directories by specifying the anme of a directoy after the command.  Be use to know whether you are using a direct or relative path.

### ls
"List".  Used to show the files and subdirectories within a directory.  If a directory is not specified, it will use the current working directory.

### man <command>
"Manual".  This is used to display the details and instructions to use any given command.  Simply type this command followed by the name of the command you wish to learns more about, and the official manual page will display.  Tip: "q" will allow you to quit from the man pages.

### cat <file>
"Concatinate".  Used to display the contents of a file.  Can also be used to edit the file.

### pwd
"Print Working Directory".  Prints to console the current directory that you are in.  Serves as a "you are here" marker.

### mkdir <name>
"Make Directory".  Create a new directory of the specified name in the current directory.

### tree

### yum
