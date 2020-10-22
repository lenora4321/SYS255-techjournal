# Lab 8 - 

## Points of interest

### Setting up and joining web server to domain

### Apache web setup

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

## Troubleshooting
automatic not manual because of dhcp
web01-lenora.lenora.local
restart httpd
