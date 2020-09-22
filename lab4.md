# Lab 3 - DHCP Server Configuration

## Points of interest

### 

## Technical Terms

### PuTTY

### Internet Explorer Enhanced security Configuration

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

### sudo -i
"Super User Do, login".  Use elevated permissions via logging in as the target user.  Allows a person to run as sudo for an extended period of time instead of having to type "sudo" before each command.

### nano
Nano is a file editor similar to VI(M).  It can be used to type, edit, and re-write files, and allows for saving them to a file location.  It is newer than VI and as such can use the arrow keys, which makes many users preffer this editor over VI.

### systemctl
"System Control".  This command is used to send insturctions to the system regarding services, like the netowrk or DHCP services.  Below are some specific commands having to do with DHCP.

**start dhcpd** Begin the dhcp service, assume it was not previously running on the device.

**status dhcpd** Check the status of the DHCP service.  Displays whether the service, what messages were sent out and with what devices the server has communicated recently.

**enable dhcpd** Set up and enable DHCP via systemlink.

The systemd control program systemctl is how you start, stop and status services.

### firewall-cmd

**--add-service=dhcp**

**--permanent**

**--reload**

**--list-all**

### ipconfig

**/all**

**/release**

**/renew**
