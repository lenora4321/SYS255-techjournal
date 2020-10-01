# Supplement 3 - Weeks 1 - 5 Overview (Steps to Rebuild)

## Lab 0 - vCenter Machines
In this lab, prep was done for the following five labs.  There were four virtual machines provided, each with a different purpose:
 - ad01: active directory comain controller
 - dhcp01: DHCP server
 - fw01: firewall
 - wks01: generic client workstation.  The virtual machines were stored within [vCenter](https://vcenter01.cyber.local/), which can only be accessed through either Champlain Campus wifi or remote VPN.
 
**Exam prep steps** connect to vCenter and ensure that all four VMs are easily locatable.

## Lab 1 - Firewall configuration and Windows setup
In this lab, the firewall was configured to connect the LAN to the outside world via WAN.  To accomplis this, the following steps were taken on fw01:

 - fw01 was virtually cabled via interface 1 to the WAN
 - interface 2 of fw01 was virtually cabled to the LAN

The fw01 workstation was then fired up and logged into via the [default passwords]().  The next step was to connect the correct networks to the correct interfaces from within the firewall.  This was done via option 1 on the fw01 firewall menu.  VLANS were not set up at this time  Option 2 was then used to set the IP addresses, including their subnet mask.  Note that the default gateway/upstream IP for the WAN was ```10.0.17.2```.

 - em0 was set to the WAN address ```10.0.17.100/24```.  Note that this is the IP assigned to the particular student for their IP address on the WAN.
 - em1 was set to the LAN address ```10.0.5.2/24```.  Note that this was the IP assigned to the default gateway of the LAN later on.

wks01 was then virtually cabled to the LAN after the initial firewall setup.  After this, a new account was made using lusrmgr.msc with consisiting of a full, dot-separated name and the postfix ```-loc```, and was then added to the administrators group form the same program.  A log off and login to the new account was performed and the eth0 adapter was configured in its TCP/IP settings to have the following data points:

 - IP: 10.0.5.100
 - Subnet mask: 255.255.255.0 (/24)
 - Default gateway: 10.0.5.2
 - Preferred DNS server: 10.0.5.2 (same as default gateway)
 
 After this, the firewall could be setup via gui from the address of the deault gateway entered in to an internet browser.  Login matched that of the pfsense console.  Using the system wizard, the following data points were set:

 - Hostname: fw01-name (Lenora was used here, recommend lower-case)
 - Domain: name.local
 - Primary DNS: 8.8.8.8 (google's public IP)
 - WAN RFC1918 networks: block private networks from entering WAN unchecked
 - Root password: set optionally
 
This made it possible to ping to various sites in a now functional network.

**Exam prep steps** 

## Lab 2 - Active Directory Domain Services and DNS setup; domain user setup
This lab set up active directory and domain name system services.  The first step to do this was to virtually cable the ad01 machine to the LAN.  After that, the server manager program was opened and the following data points configured from the local server tab:

 - IP address: 10.0.5.5
 - Netmask: 255.255.255.0 (/24)
 - Gateway: 10.0.5.2
 - DNS: 10.0.5.2 (same as default gateway)
 - DHCP disabled
 
The computer name was updated to match the patter: ad01-name (again, lenora was used).  A reboot was required to apply setting changes.  Next, ADDS was installed via "Add Roles and Features" from the "Manage" dropdown.  All defaults were followed in installation except the following:

 - Active Directory Domain Services box was checked to install

Installation required a reboot of remote server, after which promotion of the system was enacted in order to make it the domain controller.  This was found easily via the flag at the top of the Server Manager page.  The following steps were followed to do this:

 - new forest was added with root domain name ```name.local```
 - all other default options were followed, DNS error ignored
 - installation finished and system was rebooted
 
After installation, the administrator was logged into from the new ```name``` domain.  Next, DNS was to be setup by opening the Server Manager/DNS/AD01 menu.  From there, a new forward (A) address was added to the domain.  In order to make reverse (ptr) records, the "reverse lookup zones" folder had a new zone added with the network ID 10.0.5.  In total, the following records were entered:

 - (A) fw01-name: 10.0.5.2
 - (A) ad01-name: 10.0.5.5
 - (ptr) 10.0.5.2: fw01-name
 - (ptr) 10.0.5.5: ad01-name
 
The final step was to add users specific to the entire domain, not just the local computer.  To do this, the AD DS section of server manager was used to open a program called "Active Directory Users and Computers".  Under the Users folder, two new users were added.  One was added also to the Administrators group and was postifixed with the letters "adm" to denote this.  The following is a summary of the users added:

 - firstname.lastname-adm (admin)
 - firstname.lastname
 
Finally, wks01 was joined to the new domain by setting its eth0 DNS to ```10.0.5.5``` and the system properties pane was opened from control panel to change the computer name and set "member of" to domain ```name```.  The system was then restarted as a member of the new domain.
 
**Exam prep steps** 

## Lab 3 - Linux Box setup and DNS addition

**Exam prep steps** 

## Lab 4 - Linux DHCP server installation and configuration

**Exam prep steps** 

## Lab 5 - Active Directory and Domain Services and Group Policy configuration

**Exam prep steps** 

