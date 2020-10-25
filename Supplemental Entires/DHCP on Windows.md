# Supplement 4 - DHCP on Windows

## Overview
In this scenario, an urgent trouble ticket was submitted because the DHCP server, formerly run off of DHCP02 (CentOS) was removed from its location and therefore rendered inoperable on the network.  Thus, WKS02 had no IP address, since it retrieved that information dynamically from the DHCP server.  To remedy this the client wanted the service back up and running.  To solve the problem initially, a static IP address could be assigned to the WKS02 machine so that there was connectivity while the new server was being set up.  The client wanted the program up on Windows, so it was decided that the new DHCP service would be run off of FS01, or the file server.

### Roles and Features
To add DHCP onto the fs01 box, the first step was to add the new role from Server Manager on ad02.  This meant navigating to the "Add Roles and Features Wizard", selecting the desired server, and adding the DHCP role and letting it install.  Next, the tools to remotely manage it were installed from the same menu with ad02 selected--specifically, the following features:

 - DHCP Server Tools (under Remote Server Administration Tools)

### New scope setup
Once DHCP and DHCP tools were installed on their respective servers, DHCP appeared in the side navigation bar, where the DHCP Manager could be accessed from.  From there, a new scope was added by navigating to fs01 > IPv4 and right clicking to select "New Scope...".  This option opened the New Scope Wizard, where a new scope was added with the following features:

 - Name "LAN Scope"
 - Start address: 10.0.5.150
 - End address: 10.0.5.175
 - Subnet mask: 255.255.255.0
 - Lease duration: 1 hour

After the initial configuration, the next set of configurations were entered via automatic prompt.  The following configurations were added to it:

 - DNS server: 10.0.5.6
 - Default gateway: 10.0.5.2

Only after this was configured was the prompt given to actually activate the new scope.  Once activated, the addresses could be retrieved from machines like WKS02 via typical commands like ```ipconfig /renew```.  Running ```ipconfig /all``` showed that all network settings were then configured correctly once again via DHCP.  May require restart of client.

## Notes
Note that in this assignment, the student originally configured DHCP on the new Linux box web01, then moved the service to fs01.  This means that DHCP is still installed on web01; however, to prevent a conflict of IP address assignments, the service was disabled.  This may also come in handy if someone takes off with fs01 and we need a new DHCP server--all one would have to do is turn the service back on, and it's up.