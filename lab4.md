# Lab 4 - DHCP Server Configuration

## Points of interest

### DHCP configuration
In this lab, the installation of the DHCP server and its configuration were both carried out on the Linux dhcp-01 machine set up in the previous lab.  After connection to the Linux machine from ad01 via SSH and PuTTY, Yum was used to install the DHCP service package on the remote machine.

A single DHCP connection was then specified with the following details by editing the /etc/dhcp/dhcpd.conf file.  The configuration matches that displayed in the man pages for dhcpd.
 - subnet: 10.0.5.0
 - routers: 10.0.5.2
 - subnet-mask: 255.255.255.0
 - domain-name: "Lenora.local"
 - domain-name-servers: 10.0.5.5
 - range (zones): 10.0.5.100 to 10.0.5.150, totalling about 50 available host ID's.

The service was then started and enabled.

### DHCP firewal configuration
After DHCP was set up on the remote system, the firewall-cmd command was invoked to add the new dhcp service (permanently), and reload the service.  For specifics on how to do this, see the commands section below.

### Windows client configuration
After the firewall and DHCP were set up, the windows client, wks01, had to be configured to get its IP dynamically from the newly configured server.  To do this, the properties of the eth0 adapter were opened and then the properties of the IPv4 attribute, and both the IP and DNS were set to automatic instead of manual/static.

### Wireshark DHCP analysis points
DHCP messages used:
 - Release: this packet came through when the ```ipconfig /release``` command was given in the windows client, and specifies to the DHCP server that the client would like to rescind its borrowing of the IP address it had previously.
 - Discover: this message is sent out at the beginning of the ```ipconfig /renew``` command.  It is a broadcast going out from port 68 requesting a new IP address.
 - Offer: this packet is a unicast sent back to the requesting client from the server offering an IP address.  In the various header elements, there can be seen sections for the subnet-mask, the router, domain name, message type, and lease time, among other things.
 - Request: this is the reply of the client saying that it agrees to the offered terms (address) and wishes to lease it.  In here I found a lot of similar option flags to the offer message, but this time I saw mroe relating to the actual requested IP addres, such as option (50).
 - ACK: this is the final message of the interaction, wherein the server lets the client lease the address and sends this message to acknowledge it.  It again contains much of the same general information the previous few packets did, such as domain and router data.
Other:
 - Ports used: both port 67 an 68 are routinely used by DHCP, one for the client and one for the server.  In the packet capture, one can see that the ports used toggled betweent hese two as requests and replies bounced back and forth in the negotiations.
 - Unicast vs broadcast: up until the final acknowledgement, the client used broadcasts to communicate with the server, while the server replied only with unicasts.
 
### Lease time alteration
In DHCP, IP addresses are only leased for a set amount of time.  one challenge in the lab was to change this time to be a default of 1 hour and a maximum of 4 hours. This was accomplished by editing the /etc/dhcp/dhcpd.conf file yet again and adding tw lines above the initial entry:
```default-lease-time 3600;```
```max-lease-time 14400;```
I then had to refresh the services and reboot the windows client, as well as release and renew the IP address.  It is also good to note that the lease time is taken in seconds, so that is why the values may seem so large.  To view the altered lease times, I ran ipconfig /all. 

[Click to view dhcpd.conf final state](https://github.com/lenora4321/SYS255-techjournal/blob/master/Images/DHCP_conf.jpg)

## Technical Terms

### PuTTY
PuTTY is a third party software often installed on Windows machines to make it possible to connect to ther systems via SSH or TelNet.  It provides a helpful gui and terminal upon connection to the secondary system.  It contemporary rival is the newer PowerShell, which is a Windows software now upgraded with the ability to connect to SSH, among other changes.

For more information, try [this](https://the.earth.li/~sgtatham/putty/0.74/htmldoc/) resource.
*Putty Development Team, "PuTTY User Manual". PuTTY release 0.74, June 27th, 2020.*

### DHCP terms/topics
For an overview of DHCP and its description, please see [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md).  Other terminology and highlights of DHCP may be found below, with resources.  For a general overview of DHCP terms, try [this](https://browseitwebcom.wordpress.com/2018/01/04/dhcp-terminology/) resource.
*Duth, Nikhil, "DHCP Terminology".  Date not provided.*

 - DHCP scope: scope is the range of IP address a server has available to lease to prospective clients.  A DHCP server can service multiple hosts, but two DHCP servers should not service the same scope, lest a client wind up with two IP addresses and confused traffic.
 
 For more information, try [this](https://networkencyclopedia.com/dhcp-scope/) resource.
 *Network Encyclopedia, "DHCP Scope".  Date not provided.*
 
 - DHCP lease: a lease in DHCP is similar to the colloquial term "lease" in the English language, wherein a buyer can rent property from an owner for a period of time before re-negotiating the contract.  Similarly, a client (buyer) in DHCP leases an IP address from the server (owner) for a specific period of time, before the lease is either re-negotiated, renewed, or cancelled.  Note that no real currency is typically exchanged in this proceidure.
 
 For more information, try [this](https://www.efficientip.com/glossary/dhcp-lease/) resource.
 *efficient iP, "What is DHCP Lease?". Date not provided.*

 - DHCP reservation: a DHCP reservation is a feature of DHCP wherein a device can be set up to always get the same IP address form the server, whereas other addresses may change.  This is helpful for devices that are hosting services since they might be better suited with a static IP address, but are still involved in the DHCP process.
 
 For more information, try [this](https://www.stephenwagner.com/2019/05/07/static-ip-vs-dhcp-reservation/#:~:text=A%20DHCP%20Reservation%20is%20a,server%20for%20an%20IP%20address.) resource.
 *Stephen Wagner, "Static IP vs DHCP Reservation".  May 7th, 2019.*
 
## Commands

```sudo -i```
"Super User Do, login".  Use elevated permissions via logging in as the target user.  Allows a person to run as sudo for an extended period of time instead of having to type "sudo" before each command.

```nano```
Nano is a file editor similar to VI(M).  It can be used to type, edit, and re-write files, and allows for saving them to a file location.  It is newer than VI and as such can use the arrow keys, which makes many users preffer this editor over VI.

```systemctl```
"System Control".  This command is used to send insturctions to the system regarding services, like the netowrk or DHCP services.  Below are some specific commands having to do with DHCP.

 - *start dhcpd* Begin the dhcp service, assume it was not previously running on the device.
 - *status dhcpd* Check the status of the DHCP service.  Displays whether the service, what messages were sent out and with what devices the server has communicated recently.
 - *enable dhcpd* Set up and enable DHCP via systemlink.

The systemd control program systemctl is how you start, stop and status services.

```firewall-cmd```
"Firewall Command".  This is a command used to invoke Linux's firewall command line client, specifically for the firewalld daemon.  Per the man pages of any Linux system, "It provides interface to manage runtime and permanent configuration \[of the firewall\]".
 - *--add-service=dhcp* Add a service to firewall config.  Examples: DHCP, HTTP, etc.
 - *--permanent* Make a configuration change permanent, as opposed to just changing the runtime configuration.
 - *--reload* Reload the firewall service; conceivably used to shift permantant changes out into runtime by restarting runtime.
 - *--list-all* List details of firewall, including open ports and interfaces, as well as services.

```ipconfig```
Used to display information about layer 3 IP configuration, including interfaces and addresses.  When used in conjunction with options, this can also be used to alter IP connections.

 - */all* Show long version of IP configurations, including lease times.
 - */release*  Relinquish a leased IP address from DHCP server.
 - */renew*  Request a new IP address from DHCP server.
