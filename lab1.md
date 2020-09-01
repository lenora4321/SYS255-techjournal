# Lab 1 - Lab Environment Setup

## Points of interest

### vSphere
vSphere is the more web-compatible version of VMWare Workstation.  It is used to create virtual machines, run them, take snapshots, and perform other functions useful for technical operations that would be better if performed in a sandbox environment.

To get to virtual machines, go to the VMs and Templates tab at the top left.  There you will find any VMs you have or that have been created for you.  These can be powered on/off, suspended, and configured in any number of network nad hardware settings, making them very useful for networking operations testing and learning.

### fw01


### Network Configurations


### Server Configurations


## Technical Terms

### Gateway (Default Gateway)
A default gateway is a device that usually has its own IP and is used to direct packet traffic outside a given network.  The most classic example of this is a LAN with a router serving as its default gateway, where all the local devices forward their packets through the IP of the router in order to communicate with other devices.  Two default gateways were used in this lab, one coming from the student LAN at 10.0.5.2, and one coming from the SYS255 WAN at 10.0.17.2.

For more information on Default Gateways, try using [this](https://www.itpro.co.uk/network-internet/30327/what-is-a-default-gateway) resource.
*IT Pro team, "What is a default gateway?", 25 July 2019*


### Virtual Machine
A virtual machine is an operating system that runs within another operating system as a piece of software.  It borrows resources from the host when running, and can typicall be suspended or manipulated in a variety of ways.  VMs are incredibly useful as sandbox environments, functioning as a safe space to test and build without having to fear causing problems on the host machine.  In the lab, we used two VMs, one end-device running windows 10 called "wks01" and one "fw01" VM acting as the firewall between the LAN and the WAN.  This firewall was running something called pfSense.

For more information on Virtual Machines, try using [this](https://azure.microsoft.com/en-us/overview/what-is-a-virtual-machine/) resource.
*Microsoft Azure, "What is a virtual machine?", date not given*

For more information on pfSense, try using [this](https://www.pfsense.org/getting-started/) resource.
*pfsense, "Getting started", date not given*


### WAN
A Wide Area Network, or WAN, is a computer network usually consisting of multiple LANs.  This means that it can contain a number of routers and individual networks and can be used to route between networks that would previously not be able to communicate.  In this lab, the WAN used was the SYS255 WAN at the IP address 10.0.17.0/24.  It was connected to the LANs of multiple students via their assigned IP addresses for the network, provided by the instructor.

For more information about WANs, try using [this](https://www.cisco.com/c/en/us/products/switches/what-is-a-wan-wide-area-network.html) resource.
*Cisco Systems, "What is a WAN? Wide-Area Network", date not given*


### LAN
A Local Area Network, or LAN, is a computer network usually consisting of a number of individual systems, each with its own IP address (which may be a local address).  These systems can communicate with eachother usually though a switch.  A LAN is typically bounded by a single router, which funcions as a default gateway throug which all traffic outside of the LAN must pass in order to communicate between it and other networks.  In the lab, the LAN used was the STUDENTX 10.0.5.0/24 network, with a single device (a windows VM) labeled as the IP address 10.0.5.100.  This was the same for each person working on the lab, since the LAN connected to the WAN through a unique IP from the WAN IP set, as opposed to using a LAN-dependant IP.

For more information about WANs, try using [this](https://www.cisco.com/c/en/us/products/switches/what-is-a-lan-local-area-network.html) resource.
*Cisco Systems, "What is a LAN?", date not given*


## Commands

### tracert
A command used to track and report the hops taken to get from one system to another.

**-d** An option that takes a whole positive number as a parameter to specify the maximum number of hops to be attempted and recorded. *Windows*


### ping
A ping command is used to test connectivity.  It sends simple packets between two systems using the ICMP protocol.  It can then keep track of how many packets made it to and from the destination, or whether the destination was reachable at all.

**-n** An option that takes a whole positive number as a parameter to specify the number of packets to be sent and counted. *Windows*

### whoami
A command that returns the username of the current user of a system. This my be comprised of a system name and a hostname, depending upon configurations and settings.

### hostname
A command that returns the name of the system currently in use.






