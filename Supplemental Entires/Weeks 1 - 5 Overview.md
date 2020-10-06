# Supplement 3 - Weeks 1 - 5 Overview (Steps to Rebuild)

## Prelude
The following is an overview of the step-by-step instructions used to create a network with the following attributes:

 - dhcp server
 - firewall
 - active directory domain controller
 - client workstation
 - LAN/WAN connection capabilities
 - DNS lookup
 - group policies
 - domain accounts
 
After each set of instructions, a step is also included specifying potential ways in which one might get practice with the things outlined in each lab.  Please also note that the creation of this document as a whole was also used as a major review for the creator in preparation for the upcoming exam.  The target of the exam is to cre-create all the above capabilities from scratch in the alotted time (1 day).

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

The fw01 workstation was then fired up and logged into via the [default passwords](https://github.com/lenora4321/SYS255-techjournal/blob/master/Images/Default_passwords.jpg).  The next step was to connect the correct networks to the correct interfaces from within the firewall.  This was done via option 1 on the fw01 firewall menu.  VLANS were not set up at this time  Option 2 was then used to set the IP addresses, including their subnet mask.  Note that the default gateway/upstream IP for the WAN was ```10.0.17.2```.

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

**Exam prep steps** Switch cabling on fw01 to WAN and then back to LAN.  Using options 1 and 2 from the fw01 menu, change the assignments of em0 and em1, change their associated network information, and then fix it so that pinging is once again possible between the associated machines.

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
 
**Exam prep steps** Add new DNS records or erase the existing ones and re-create them in ad01.  Add 2 new users, one with elevated privledges and one without, then join the ```name``` domain.

## Lab 3 - Linux Box setup and DNS addition
This lab began by stting up the Linux CentOS box that was the be the future DHCP server with its own IP address and network information.  Using the command nmtui and the visual user interface it generated, the following netowrk settings were associated with the ```ens192``` network:

 - IP address: 10.0.5.3/24 (CIDR netmask included)
 - Gateway: 10.0.5.2
 - DNS Server(s): 10.0.5.5
 - Search domain(s): name.local
 
After this, a restart of the network service was required, and the hostname was changed to ```dhcp01-name```.  A privledged user was then added to the wheel group under the convention ```name-adm``` as before.  As specified in lab 2, DNS A and PTR records were added to accomodate the new system as follows:

 - (A) dhcp01-name: 10.0.5.3
 - (ptr) 10.0.5.3: dhcp01-name

After this, it was possible to connect to the DHCP VM via SSH from ad01.

**Exam prep steps** Clear out the network settings from nmtui and re-enter them.  Change the hostname on the DHCP VM and add an elevated user.  Practice connecting via SSH from ad01.

## Lab 4 - Linux DHCP server installation and configuration
The first step to this lab was turning off Internet Explorer Security COnfiguration for Adminstrators, in order to make it possible to do the subsequent tasks in the lab.  Most of the following steps were then done via SSH to the dhcp server.

The dhcp service was installed via yum and the ```/etc/dhcp/dhcpd.conf``` file was edited to the final state (note that default lease times were also changed) reflected in [this](https://github.com/lenora4321/SYS255-techjournal/blob/master/Images/DHCP_conf.jpg) image from lab 4. The following things were then done via command to enable dhcp to work properly:

 - dhcp service started
 - dhcp service enabled
 - dhcp service permanetly added to firewall
 - firewall realoaded
 
After exiting SSH, wks01 was then re-configured via adapter tcp/ipv4 properties to use dhcp instead of the static IP addresses assigned in earlier steps.  Finally, the lease time was changed on the dhcp server, as noted and reflected in the picture linked above. 

**Exam prep steps** Stop the dhcp service.  Clear out the config file and re-enter the settings.  Start the service again.  Practice locating the adapter properties to switch from static to dynamic IP addressing on wks01.

## Lab 5 - Active Directory and Domain Services and Group Policy configuration
In this lab, Active Directory Users and COmputers was opened from the tools tab of the server manager.  Four new OUs were added, as described below:

 - SYS255
 - Accounts (nested in SYS255)
 - Computers (nested in SYS255)
 - Groups (nested in SYS255)

The following users and computers were then added/arranged in the OU's as detailed below:

 - New user alice added to Accounts
 - New user bob added to Accounts
 - New user charlie added to Accounts
 - Computer WKS01-name moved from Computers folder to Computers OU
 - New group ```custom-desktop``` created in Groups.
 
Users alice and bob were then added to the new group.  After that, the group was configured via the Group Policy Management tool from Server Manager in the following ways:

 - GPO added to SYS255
 - GPO group ```Authenticated Users``` removed from security filtering
 - GPO group ```Domain Computers``` added to security filtering
 - Apply gorup policy denied from Delegation tab for ```Domain Computers```

The Group Policy Editor was then used to configure the following rules for users and computers, as denoted below (note that for the second point, a new GPO was created to accomodate the rule):

 - Remove Recycle Bin icon from desktop enabled for users in the ```custom-desktop``` group
 - Interactive logon: Don't display last signed-in enabled for computers in ```Computers```, of which there is currently only one.
 
To finish off and test new policies, gpupdate /force and reboot were both used.

**Exam prep steps** Add a new user to Accounts and a new group to Groups, then add the user to Groups.  Give the user a new GPO rule specifying something interesting, such as changing the desktop background image.  Then create a new rule for the Computer OU specifying a new setting for computers associated with it.
