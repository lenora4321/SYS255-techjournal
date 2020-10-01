# Lab 2 - Active Directory and DNS

## Points of interest

### Active Directory
In this lab, several users were added and managed using an Active Directory through Windows Server Manager.  This was useful because normally a new system has to have at least one adminstrator account with outrageous permissions, but managing it with an active directory instead can give sensible admin privledges and manage users remotely.  The following users were added with the given permissions in this lab:
 - lenora.batcher-amd (admin)
 - lenora.batcher (regular user)
They were both added to a domain called simply "lenora"; however, the admin account, denoted with the -adm after the name, was also added to the Domain Admin group from the Active Directory Users and COmputers Program found on Windows 10.  The computer used to control the active directory primarily was the ad01-lenora.batcher, and this is where the Active Directory was configured from.


### DNS
In this lab, a DNS server was configured to connect out from the system wsk01-lenora.  For details on what DNS is, see the Tech Terms section below.  To set up the DNS server, Windows Server Manager was used to configure roles and add Active Directory capabilities.  After that, the DNS Manager program on Windows 10 was use to configure the DNS server by manually adding in host (A) records that returned IP addresses for given hostnames, and the opposite for reverse lookup (ptr) records.  The following records were manually entered:
 - ad01-lenora
 - fw01-lenora
This allowed the user to ping from the host machine directly to human-friendly host and domain names to make communication within networks more easy for the user.

## Technical Terms

### DNS 
The acronym DNS stands for "Domain Name System".  It a network's way of translating between hostnames (like www.google.com) and IP addresses (like 8.8.8.8).  All websites and systems are typically known by their IP addresses in order to navigate between them; however, humans don't tend to be the best at memorizing strings of numbers.  DNS makes it so that humans can type in a hostname and the computer looks up the IP using DNS so that it can find the correct resource and display it back from  behind the scenes, so the user never has to worry about the IP address.

For more information on DNS, try [this](https://www.cloudflare.com/learning/dns/what-is-dns/) resource.
*CloudFlare, "What Is DNS? | How DNS Works", date not provided*

### Active Directory
An active directory is a system and its configurations that allows for a network/domain to create, manage, and grant permissions to multiple users.  These users are typically organized into three tiers: 
 - Domain: users an close systems are grouped under a domain
 - Tree: several domains can be grouped into a tree
 - Forest: several trees can be grouped into a forest
Access rights and privledges for certain files and actions can then be delegated base upon certain users and their place within the active directory.  This type of organization is usually associated with Windows and their software for it, called "Active Directory".

For more information on Active Directory, try [this](https://techterms.com/definition/active_directory) resource.
*Tech Terms, "Active Directory", July 13, 2017*

### Windows Server Manager
Windows Server Manager is a piece of Miscrosoft software used to manage both remote and local servers, as well as the roles of user accounts on those servers, from one more centralized location.

For more information on Windows Server Manager, try [this](https://searchwindowsserver.techtarget.com/definition/Microsoft-Windows-Server-Manager) resource.
*Margaret Rouse et al., "Microsoft Windows Server Manager", February 2016*

### IP address (IPv4)
An IP address is a 32-bit number, typically divided up into 4 8-bit sections, that allows for devices to be referenced and communicated with over the Internet Protocol.  An IP address is typically unique either to a device or to a network that uses a single device through which to direct all its traffic, assigning a re-usable set of private addresses within and sharing one public address to communicate without.  An IP address is a combination of two numbers, both a network address and a hostID.  The network address takes a number of the bits from the front of the IP address (as determined by the network mask, a series of numbers resembling an IP address used to separate net and host ID's) to signify what network an address is part of, delegating the remaining numbers as the hostID, which unquiely identifies each device on the network.  IP addresses are commonly associated with layer 3 of the OSI model, or the "network layer", as well as with routers.

For more information on IP Addresses (IPv4), try [this](https://www.ripe.net/about-us/press-centre/understanding-ip-addressing) resource.
*Ripe Network Coordination Center, "Understanding IP Addressing and CIDR Charts", August 9, 2019*

### Hostname
A hostname is a human-fiendly title that references a particular system.  This hostname can be resolved to an IP address using DNS, described above.  An example of a hostname is "www.google.com" or "localhost".  These hostnames may be broken up around a dot to signify domains and help DNS to locate and return the correct IP address.

For more information about Hostnames, try [this](https://en.ryte.com/wiki/Hostname#:~:text=A%20hostname%20is%20a%20unique,multiple%20domains%20under%20one%20host.) resource.
*Ryte Wiki, "Hostname", date not provided*

### Domain Users (contrary to regular local users)
Domain users are users who are not associated with a particular computer system, but rather are members of a domain which controlls thier permissions.  That user can be loged into any correctly configured computer, but it must be connected to its domain controller in order for it to verify passwords and set permissions locally for that login session.  This type of account is more common across large distributed domains or even smaller domains that need to be spread across multiple systems or dealt with remotely.

For more information on Domain Users, try [this](https://kb.iu.edu/d/anbn) resource.
*Indiana University Knowledge Base, "Local users and domain users in Windows", February 7, 2020*


## Commands

```nslookup```
This command attempts to retrieve the IP address of a provided hostname, whether from DNS cache or via DNS lookup.

*Other useful commands may be found in [lab1](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab1.md) commands section.*
