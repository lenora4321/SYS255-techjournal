# Lab 3 - DHCP Linux Box Setup

## Points of interest

### Cabling re-cap
This lab was run totally on VMs, as all labs from this course will be.  This means that all "cabling" for ethernet was actually done via virtual connections in virtual machine software, specifically VSphere.  All systems were turned on and "cabled" by switching their network to SYS255-02-LAN-lenora.batcher, or the local LAN that was the object of the labs.

### nmtui Network Setup (Static IP in CentOS)
There are a few ways to set up an internet connection via static IP on CentOS, but the one recorded here is perhaps the simplest, as others involve directly editing the config files of the system.  Instead, a tool called nmtui (defined in more detail under the "commands" section below) is used as a more clear-cut, user-friendly method.  The steps to set up a static IPv4 address are outlined below.
 1. enter command "nmtui" in terminal
 2. select the "edit a connection" option by highlighting it and pressing enter
 3. select the connection you wish to modify (in this case, ens192)
 4. navigate down to the IPv4 section and enter the following settings:
	- Address: IPv4 address separated by dots with cidr notation for subnet.  Address used for this lab was 10.0.5.3/24.
	- Gateway: IPv4 default gateway address.  This lab used 10.0.5.2.
	- DNS servers: enter any DNS servers in IPv4 format.  This lab used 10.0.5.5
	- Search domains: enter any domains connected to for searching, etc.  This lab used the previously created domain of lenora.local
	
 5. leave other settings at default and select <OK> at the bottom of the screen to exit.
 6. restart network services by entering the command ```systemctl restart network```. 

## Technical Terms

### SSH
SSH stands for "Secure SHell" and is the way that most UNIX-based operating systems connect remotely for control of a shell operated on the remote system.  The precursor to this protocol was TelNet, which was not encrypted or "secured" the way that SSH is, and so was phased out in favor of the new.  The way to initiate such a connection is to use the command "SSH" in conjunction with a destination and log in with valid credentials.

SSH can be used on Linux and now Windows with the new implementation of powershell.  Before powershell, the tool commonly used on Windows was a third party application called PuTTY.

For more information about SSH, try [this](https://www.ssh.com/ssh/#the-ssh-protocol) resource.
*ssh.com, "SSH (Secure Shell), The SSH Protocol". Date not provided.*

### DHCP
DHCP stands for "Dynamic Host Configuration Protocol", and is a way of automatically managing networked devices, specifically via the layer 3 protocol Internet Protocol.  Instead of statically setting an IP address for a host system, the system can request one from a server that is supplied dynamically depending upon availability, among other things.  The basic process works like this:
 1. Host system broadcasts that it needs an IP address
 2. DHCP server sends back a potential address
 3. Host system requests to lease the address for a certain period of time
 4. Server agrees and the IP address is then in use
This is makes setup and configuration much easier on the administrative side, and much more flexible as well.

For more information, try [this](https://www.efficientip.com/what-is-dhcp-and-why-is-it-important/) resource or [this](https://www.youtube.com/watch?v=S43CFcpOZSI&feature=youtu.be) resource.
*Efficient iP, "What is DHCP?".  Date not provided.*
*CertBros, "DHCP Explained | Step by Step". January 4th, 2017*

### Linux
Linux is an operating system popular on servers and desktops alike for its free open source, and lightweight implementation.  It was created by Linus Torvalds in 1991 and is an descendant of UNIX and a close descendant of Minix.

For more information, try [this](https://www.linux.com/what-is-linux/) resource, or find the source code itself anywhere code repositories are distributed.
*The Linux Foundation, "What Is Linux?" linux.com, date not provided.*

## Commands

### nmtui
"Network Manager Text User Interface".  A visual interface for configuring network settings on Linux.  Functions in the command line with simple prompts and options allowing for activities like setting a static IP or connecting to DHCP.

### adduser <name>
"Add user".  Create a new user of the given name.  User will be added to a group of their own name, but no other groups.

### passwd <name>
"Password".  Change the password for a given username.  If there is already a password set, it will likely ask for the old password.  Will require password to be retyped for certainty.

### systemctl restart network
"System Control" setting to restart the network service.  Should be done after an update is made to netowrk configurations.

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
The tree command prints the contents of directories in a tree-like format, which can be more visually easier to work with than the traditional text format.  Starts at the current directory and prints supdirectories and files.

### yum
"Yellowdog Updater, Modified".  A tool for installing and maintaining packages originally developed for Yellowdog Linux.

For more information, try [this](https://webhome.phy.duke.edu/~rgb/General/yum_HOWTO/yum_HOWTO/yum_HOWTO-1.html) resource.

*Brown, Robert G., et al. "Yum (Yellowdog Updater, Modified) HOWTO, Introduction". September 24th, 2003"

