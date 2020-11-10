# Supplement 5 - WordPress Configuration Resources

## Overview
WordPress is a content management tool that can be installed on a Linux as well as a PC system.  I installed it on web01 for practice.  It required also a LAMP, which basically means Linux (the OS, already had), Apache (web server, already had), MySQL (installed with MariaDB), PHP (already had, but updated to PHP 7.2 for this exercise).  The installation and setup is very similar to the Windows XAMPP work I've done in the past with Laravel for web app creation.

## Resources (links)
Most of the steps I followed to make a new blog site were found off of the internet.  Below are some of the sites referenced that could be very useful in recreating such a blog site for the future.

 - [Installation on CentOS7](https://www.liquidweb.com/kb/how-to-install-wordpress-on-centos-7/).  *Michelle Almendarez, "How to Install WordPress on CentOS7". Liquid Web, October 26, 2020.*
 - [WordPress CLI installation](https://wp-cli.org/#installing).  *WP CLI, "Installtion".  Date not provided.*

## Setup steps for a new web linux box (blog01)
Below are a few short steps to create the blog01 machine with a LAMP stack to support WordPress.  Note that these are general instructions, not step-by-step.  Please refer to [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md) and [lab 8](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab8.md), as well as the resources above, for more specific instructions.
 1. Connect system to proper LAN network
 2. Configure NMTUI with proper IP address, gateway, hostname, netmask, etc.
 3. Create a named sudo user by adding them to the wheel group
 4. Edit the SSH config file to secure SSH remoting
 5. Install realmd and supporting packages, then join box to Active Directory
 6. Yum install httpd for apache
 7. Go through steps to install PHP 7+
 8. Allow Apache through firewall
 9. Install MySQL
 10. Install WordPress
 11. Configure MySQL tables to accomodate WordPress
 12.  Check connectivity form wks machine, configure from there if successful