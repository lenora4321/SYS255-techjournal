# Supplement 1 - Linux File and Directory Permissions

## Overview
In the Linux operating system, nearly everything stored within is either a file or a directory.  One of the selling points of the operating system was that it had multiple users, making it much more efficient for remote connection as well as direct usage for multiple people.  But with multiple users comes the issue of permissions--that is, access access rights for files and directories in order to uphold values of privacy and security.

Listed below is the basic layout of Linux file and directory permissions, excluding special bits (but offering further resources for those interested).  The points of interest are divided up into two categories: who (who has a permission), and what (what permississions do they have), followed by a section on commands to assign permissions.

For more information on the topics outlined below, try [this](https://www.linux.com/training-tutorials/understanding-linux-file-permissions/) resource.
*mfillpot, "Understanding Linux File Permissions".  Linux.com, May 18th, 2018.*

### Users, groups, and others
In Linux, every file and directory has is created with respect to three different access levels, detailed below.  Each access level can be assigned different permissions, giving the users at that level different abilities regarding the files in question depending upon which of the three categories they fall under.

 1. User: the user in Linux is another term for the owner of a file.  Reffered to in abbreviation as "u", this person is usually the creator of the file and the one with the highest permissions regarding it, but not always (and it can be changed at any time).  This permission level will always be occupied by a single Linux user, as found in the user management file in /etc/passwd.
 2. Group: in Linux, a group is made up of a collection of users and is referred to by a name or an id similar to how a user is referred to in the operating system.  Groups are typically found in the /etc/group file.  Abbreviated as permission "g", each file has a group to which it belongs, and is by default usually set to the group of the user upon creation.  Group access can be configured to give each member of the group certain permissions regarding a file, while higher permissions (or lower, depending upon intent) can still be delegated to the single owner of the file.  For example, user "bob", a member of group "alpha", might not be the owner of a file, but he still has access to it because the group of the file is set to "alpha" and its permissions allow said members to view it.
 3. Others: others in Linux stands for any other users that do not fall under one of the previous two categories, either the owner (user) or the group.  SUch users typically have the lowerst permissions of access, though this can vary with intent.  Anyone not in the group or who is not the user will fall under this category and get whatever permissions are allocated to it.
 
### Access levels and abilities
In Linux, there are three different types of access permission a given user can have regarding a file.  Combined with the person's status in regards to the user, group, and others of the file/directory, an effective system of protection and privacy can be implemented.  Below are detailed the different permission types:

 1. Read: this permission, abbreviated "r" allows a user to access and view a file.  It alone does not allow changes to be made to the file.
 2. Write: this permission, abbreviated "w" allows a user to make changes to a file, such as with a text editor or the redirected ```cat``` command.
 3. Execute: this permission, abbreviated "x" allows a user to run a file, as though it were an executable file type.  This is usually only useful for executable files, but can be set for most any files.
 
Note that the executable bit cannot be set for a directory, which usually has its own "d" or "directory" bit set to differentiate it from files.

## Commands

### chmod
"Change mode".  This command is used to change the permissions of a file or directory.  It can take either an octal value (detailed later) or letter abbreviations.  When invoked with the permission specifications and the name of a file (may require sudo, depening upon user doing the changing), it can set the permissions for each group.  See example below:

```chmod u+w example.txt```  This will give the user the write permission on the file example.txt.
```chmod 664 example.txt```  This will give the user and group read and write permissions, and all others only permission to read file example.txt.

### chown
"Change owner".  This command is used to change the owner of a file or directory, though it may also take the group group parameter and change it as well.  May require sudo.  See example below:
```chown bob example.txt```  This will change the owner (user) of file example.txt to bob.

### chgrp
"Change group".  This command is used to alter the group of a file or directory.  May require sudo.  See example below:
```chgrp admin_group example.txt```  This will change the group of the example.txt file to the group admin_group.

## Notes

### +, =, -
In chmod, permissions can be either added (+), taken away (-), or set equal to (=) a given abbreviated access level.  Used in conjunction with a letter for the recipient and a letter (or more) for the access level.  See examples below:
```u+w```  Add write permission to user.
```g-r```  Remove read permission to group.
```o=rwx```  Set the permissions for others to read, write, and execute.

### Octal permissions
Alternatively, permissions can also be specified using an octal code for things like chmod and the default mask (a code which sets the default permissions for a new file).  This notation is similar to the "=" from the abbreviated notation, except that it is used to set all different access levels at once.  In this notation, the options can be any octal code (from 0 to 7), which specify what that level can do with a file.  In the bit settings, 4 is a read, 2 is a write, and 1 is an execute.  Three numbers are specified at once, each digit corresponding to user, group, or others, in that order.  See examples below:
```777```  This will give full permissions (rwx) to all three access levels: user, group, and other.
```664```  This will give the user and group read/write permissions, and all others only read permissions.
```001```  This will give the others permission to execute the file only, while user and group cannot access the file at all.

### Special bits
In the newer numbering system used to denote permissions, there are more bits than are accounted for in this brief summary.  The remaining bits are often referred to as "special bits", and can include the sticky bit and T bit, among others.

For more information on special bits, try [this](https://linuxconfig.org/how-to-use-special-permissions-the-setuid-setgid-and-sticky-bits) resource.
*Docile, Egidio, "How to use special permissions: the setuid, setgid and sticky bits".  LinuxConfig.org, June 8th, 2018.*