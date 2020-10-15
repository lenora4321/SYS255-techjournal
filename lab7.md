# Lab 7 - Server Core and Remote Administrator Tools

## Points of interest

### Configuration of file server, including sconfig tool
In this lab, a file server, later named FS01-lenora, was cabled (virtually) to the LAN and added to the lenora domain.  Pointer and A records (see [lab 5](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab5.md) ) were also created for this new machine.  Network, as well as hostname, configuration were all done from a built-in UI tool found in Windows Server Core invoked with the command sconfig.  The following were entered as the specs for this new machine:
 - IP: 10.0.5.8
 - Subnet Mask: 255.255.255 (/24)
 - Default Gateway: 10.0.5.2
 - DNS Server: 10.0.5.6
 - Server name: FS01-lenora
 - Domain: lenora

### File Service Tools
To properly enable the file server to function on the domain, as well as to control it via the GUI machine remotely, a feature was first added to ad02 via the Add Roles and Features wizard.  The boxes checked to do this were:

 - File Services Tools
 - File Server Resource Manager Tools

The file server was then added in and ad02 configured with OU structures as outlined in the section below.  After that, the File Server Resource Manger feature was directly added to the fs01 server.  Once it was allowed through the firewall, a quickshare could be made on the file server and configured to let the group "sales-users" have full control.  This allowed only those users in the security group to access the files there.

### OU structure
Several Organizational Units were added to the domain to support the structure of the activities done in the lab.  As noted below, several users and groups were also added to the same end.  These OU's were added specifically to the active directory at ad02.

**OU's**
 - SYS-255
 - Users
 - Groups
 - Computer

**Objects**
 - Users "alice" and "bob" were both added to the "Users" OU
 - Group "sales-users" was added to the "groups" OU

After this setup, user alice was assigned to the "sales-users" group, while bob was not.

### S:\ drive map
In order to map a share to a certain secuity group's drive letter, execute the following steps (assumes the share itself is already configured to be accessbile from the group's systems).
 1. Create Group Policy Object in an OU with access to the desired group (SYS255 used in this lab)
 2. Ensure that Authenticated Users is in the security filtering.  This will be altered later to be applied only to one security group, but all must first be in this filtering for it to work
 3. Edit the GPO and navigate to UserConfig > Preferences > Windows Settings > Drive Maps
 4. Right click on Drive Maps and do "create new"
 5. Enter the following data:
 - Type: create
 - Location: \\fs01-lenora\Sales (or wherever the share is located, with universal naming convention is best)
 - Letter: for this lab, "S" was used
 - Options: show this drive and show all drives
 - On the Common tab, select the following:
	- run in logged-on user's security context
	- item-level targeting > targeting > remove/add so that only security group is included > add desired group (sales-users was used in this lab)
 6. Log out and in again on an account in the correct group and check drives from file explorer to see new drive
 
For more details and step-by-step walkthroughs on how to do map drives with group policies, try any of the following three resources:
 - [A](https://activedirectorypro.com/map-network-drives-with-group-policy/) *Allen, Robert, "How To Map Network Drives With Group Policy (Complete Guide)". Active Directory Pro, July 13, 2018*
 - [B](https://blogs.manageengine.com/active-directory/active-directory-academy/2019/11/18/mapping-drives-using-group-policy-preferences.html) *Active Directory Academy, "Mapping drives using Group Policy preferences".  Manage Engine Blog, November 18, 2019*
 - [C](https://www.faqforge.com/windows/map-shared-folder-network-drive-using-group-policy/) *Buzdar, Karim, "How to Map a Shared Folder to Network Drive Using Group Policy".  FAQ Forge, date not provided*
 
## Technical Terms

### Windows Server Core
Windows Server Core is a lighter, more efficient version of Windows Server that was designed to implement all the same features but without the GUI.  Because of this, it takes significantly less resources to operate.  It can also still be linked with the Windows Server itself and be operated via GUI from there, making it optimal to have for those who preffer a mix of server and GUI.  In this lab, the Core was used as a file server and linked to the original domain controller to operate most of the commands via GUI.

For more information about Windows Server Core, try [this](https://www.webopedia.com/TERM/S/server-core.html) resource.
*Stroud, Forrest, "Server Core".  Webopedia, date not provided.*

### File Server

### Windows permissions:
In Windows, unlike Linux, there are two kinds of permissions that can be used to selectivley allow access to files and resources on a device.  Below is given a breif summary of each.  Note that when both are applied, the stricter set will be enforced upon the users.

 - NFTS: Meaning "New Technology File System", this set of permissions is applied locally on a computer to files stored there.  Its permission levels, described in more detail in the source below, are: full control, modify, read & execute, read, and write.
 - Share: Shares are used to set permissions on remote files accessed through a network.  Also described in more detail in the external resource, its permissions are: full control, change, and read.
 
For more information about Windows permissions, try [this](https://blog.netwrix.com/2018/05/03/differences-between-share-and-ntfs-permissions/) resource.  Provided by instructor.
*Melnick, Jeff, "Differences Between Share and NTFS Permissions".  Netwrix blog, May 3, 2018*
 
### Universal Naming Convention (UNC)
The Universal Naming Convention is a way to access shares without actually specifying the drives and location of a file or folder on a computer.  it commonly uses two back slashes ```\\``` followed by the desired file path, such as ```\\fs01-lenora\Sales```, the example used in this lab.

For more information about the UNC, try [this](https://whatis.techtarget.com/definition/Universal-Naming-Convention-UNC) resource.
*Rouse, Margaret, "Universal Naming Convention (UNC)".  Tech Target, April 2005*

## Commands

```sconfig``` This command invokes a UI configuration tool for setting network and other system configurations on a Windows Server Core machine.  It provides a list of numbered options for the user to choose from and can set domain, IP address, and system name, among many other things.

```\\fs01-lenora\sales``` This "command" is really just the location of a file folder on a Windows PC, named with the universal naming convention.  When typed into a command prompt, it can be used to test whether or not a user has access to that file folder, since it will respond with a "denied" message if they do not.

```netsh advfirewall firewall set rule group=”Remote File Server Resource Manager Management” new enable=yes```  This command is just a command-line version of a new rule being added to the firewall to allow remote file server resource management through.  In this lab, it was run directly on the fs01 file server.


