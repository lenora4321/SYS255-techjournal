# Lab 1 - Lab Environment Setup

[Click to view provided server diagram](https://github.com/lenora4321/SYS255-techjournal/blob/master/Images/Lab1_diagram.png)

## Points of interest

### vSphere
vSphere is the more web-compatible version of VMWare Workstation.  It is used to create virtual machines, run them, take snapshots, and perform other functions useful for technical operations that would be better if performed in a sandbox environment.

To get to virtual machines, go to the VMs and Templates tab at the top left.  There you will find any VMs you have or that have been created for you.  These can be powered on/off, suspended, and configured in any number of network nad hardware settings, making them very useful for networking operations testing and learning.

### fw01
In the lab, one VM used was titled fw01.  It was a pfSense firewall that also served to provide routing between our local LAN and WAN.  One of the first steps was to set this up so that the packets sent from the end device on the LAN could actually make it out and access the SYS255 network, through which the packets could later be routed out onto the cyber network and access the internet.  The first step was to set up the two networks for this VM by going to "settings" from the vSphere page.  Frome there, it was virtually "cabled" to both the LAN and the WAN.  Upon startup, the VM then presented a list of options to configure the firewall, the details of which are included in the "Network Configurations" section of this document.


### Network & Server Configurations
In this lab, there were a total of three networks provided, plus the internet.  From the top down, those networks are as follows:
 - CYBER: 192.168.4.0/24
 - SYS255-WAN: 10.0.17.0/24; default gateway @ 10.0.17.2
 - STUDENTX: 10.0.5.0/24; default gateway @ 10.0.5.2
The lab only ever required us to configure the last two networks, the student LAN and the class WAN.  On the LAN, each student had one end-device running windows 10 called "wks01" at IP 10.0.5.100.  On the WAN, each student had a connecting IP addres of 10.0.17.1XX, where XX was replaced by the instructor-assigned station number.  Using the options porvided in fw01, the WAN was assigned to "em0", virtually cabling it to that interface, and the LAN was assigned to "em1"  From there, IP addresses were assigned to using option 2 on the pfsense web terminal:
 - WAN/em0: 10.0.17.1XX, no DHCP, no HTTP
 - LAN/em1: 10.0.5.2 (the default gateway), no DHCP, no HTTP
On the end device, wks01, the IP address was set to the 10.0.5.100 address as mentioned above, and the default gateway also set to match the 10.0.5.2 address given above.

### GUI Configurations
The following are the last few configurations as done from the address of the LAN default gateway, 10.0.5.2, in a web browser, ignoring security certificate errors as directed.
 - hostname: fw1-lenora
 - domain: lenora.local
 - Primary DNS: 8.8.8.8 (google's public dns)
 - Block private networks from entering via "WAN": unchecked


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


### Firewall
A firewall is a piece of technology, usually software-based, that sites between two devices or networks.  It is used to secure one or both sides of the connection by limiting what packets travel between them.  This is done most commonly via a set of simple allow or deny rules, where a packet is either allowed in or dropped/rejected depending upon how it fits certain criteria.  These criteria can be as simple as what IP is sending a packet, or can get much more in-depth and work with protocols and signatures, and beyond.  Firewalls usually come with default setings, though they can be manipulated by their owner to allow or deny certain types of traffic depending upon user needs.

For more information about firewalls, try using [this](https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-firewall.html) resource.
*Cisco Systems, "What Is a Firewall?", date not given.*


## Commands

```tracert```
A command used to track and report the hops taken to get from one system to another.

 - *-d* An option that takes a whole positive number as a parameter to specify the maximum number of hops to be attempted and recorded. *Windows*


```ping```
A ping command is used to test connectivity.  It sends simple packets between two systems using the ICMP protocol.  It can then keep track of how many packets made it to and from the destination, or whether the destination was reachable at all.

 - *-n* An option that takes a whole positive number as a parameter to specify the number of packets to be sent and counted. *Windows*

```whoami```
A command that returns the username of the current user of a system. This my be comprised of a system name and a hostname, depending upon configurations and settings.

```hostname```
A command that returns the name of the system currently in use.






