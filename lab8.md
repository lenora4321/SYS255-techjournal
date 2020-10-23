# Lab 8 - Apache Web Server

## Points of interest

### Setting up and joining web server to domain
For this lab, a CentOS machine was added to the network and configured very similarly to the way the DHCP server system was configured in [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md).  It was virtually cabled to the LAN and assigned static IP address information as recorded below.  It it also worth noting that the IP address used in this lab may be the same one as used to initially configure other systems on the LAN; this is due to the fact that the DHCP server was removed as part of an earlier assignment, freeing up the IP address.  DHCP was moved to another system, and the box was not recreated.

 - IP address: 10.0.5.4/24
 - Gateway: 10.0.5.2
 - DNS server: 10.0.5.6
 - Search domain: lenora.local
 - Hostname: web01-lenora.lenora.local

To join the Linux box to the Windows Active Directory, realmd was installed along with the following supporting packages using ```yum install```

 - realmd
 - samba
 - samba-common
 - oddjob
 - oddjob-mkhomedir
 - sssd

Using the ```realm join``` command (as detailed in the commands section below), the box was joined to the domain "lenora.local" with the named adm user from the Active Directory.  After logging off, this user could then be signed into the account from the web01-lenora box just like it could be on a Windows box.

### Apache web setup
After initial setup and a restart of the network service, ```yum install``` was used to install apache web server (httpd package) onto the new machine.  This also required http to be allowed through the firewall, using a command similar to the one found in, again, [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md).  Then, the default web page could be navigated to from wks01 or any other machine on the network with the ability to render web pages.  To remove the default screen, the instructions on said screen were followed to comment out all the lines in the welcome.conf file for apache.  Two new files could then be added in the following locations:

 - /var/www/html/index.html
 - /var/www/html/index.php

Both were filled with basic markup/code from the languages that corresponded to their file endings.  In order to get PHP to render in a web page, ```yum install php``` was run on the system, and the httpd service was restarted. 

## Technical Terms

### Apache (web server)
Apache is a web server project closely associated with Linux that is free and open-source.  It supports Windows and UNIX and provides for the ability to support HTTP requests and traffic, which provides for the rendering of web pages that make up the familiar gui-based side of the modern internet.  Apache currently has one of the biggest market shares in the web server world.

For more information on Apache, or to contribute to the project, try [this](https://httpd.apache.org/) resource.
*Apache Software Foundation, "Apache HTTP Project".  Date not provided.* 

### Realmd
Realmd is a program that allows Linux boxes to join a Windows Active directory.  This is huge, because previously one had to have a Linux and a Windows set of permissions and rules that were managed and stored separately, whereas now they can be managed together.  The program can easily be installed on a Linux machine using a package installer, and commands such as ```realm join``` are issued to join a domain.  Note that the local Linux users are not involved in the active directory, but named domain users can now log in onto the Linux system with their domain credentials.

For more information about realmd, try [this](https://www.freedesktop.org/software/realmd/) resource.
*Free desktop.org, "realmd".  Date not provided*

### Web scripting/programming languages
To present the visual, functional collection of documents that we call the web, a number of different languages are used to control every each level of computing.  While other langauges can certainly be used, those below are commonly used in the web setting to render web pages.

 - PHP (PHP Hypertext Processor) programming language usually used for server side computing in a web server
 - HTML (Hyper Text Markup Language) markup lanugage used to arrange elements on a web page
 - CSS (Cascading Style Sheets) style markup for HTML layered in 3 levels: inline, embedded, and external
 - JS (JavaScript) client-side programming language used to control functionality on a web page

For more information on web scripting, try [this](https://www.thesitewizard.com/html-tutorial/what-is-html.shtml) resource.
*Christopher Heng, "What are HTML, CSS, JavaScript, PHP and Perl? Do I Need to Learn Them to Create a Website?"  The Site Wizard, January 6, 2020.*

For tutorials on how to use any of the above languages, try [this](https://www.w3schools.com/howto/default_page4.asp) resource.
*w3shools, "W3Schools How To".  Date not provided.*

## Commands
```realm join``` command used to locate, process, and join a domain.  Run on a Linux machine to join an active directory.

 - *--user=<username@domain>* include this option to join the specified domain with the specified user.

```real list``` command to list out all "realms" (domains) that a Linux box is a part of (must have realmd installed).

```firewall-cmd``` used to allow http through the firewall using the exact same sequence of commands as used in [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md) to allow dhcp through the firewall, except that "dhcp" was switched out with "http".  Note that this also could have been achieved by allowing specific ports, namely 80 and 443 (responsible for web traffic; TCP), through the firewall instead of just the service itself.

## Troubleshooting

### DNS failure to resolve
If you are experiencing issues resolving DNS queries on the new machine, but are still able to ping the other devices on the netwrok, consider that the issue may be with one of the following misconfigurations:

 - Automatic IP assignment still set in nmtui even though static addresses are assigned
 - Misconfigured host name: should be web01-lenora.lenora.local
 - restart network service

### PHP not loading
If, after installing PHP onto the web server, you attempt to render a page and notice that the PHP code appears to come back in plain text, attempt the following step to fix it:

 - Restart httpd service
