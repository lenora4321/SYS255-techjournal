# Supplement 1 - Securing CentOS SSH (root block)

## Overview
In a world of remote connections and security, it is best practice to make it so that the root user (the one with the highest permissions of all on a device) cannot be accessed by anyone other than someone directly at the system itself.  This prevents against a number of cyber attacks and is implemented on Linux CentOS quite easily.  See the steps below.

 1. Have your sudo password ready, since most of these commands will require elevated privledges.
 2. Open the config file for Linux SSH in a text editor like nano, using a command similar to: ```sudo cat /etc/ssh/sshd_config```.
 3. Navigate to the line that says ```#PermitRootLogin yes``` and change it to ```PermitRootLogin no```.  This will uncomment the line and change the setting so that remote login to root via SSH is prohibited.
 4. Save the file and close the text editor.
 5. Restart the SSH service via the command ```sudo systemctl restart sshd```.

After these steps are carried out, attempt to conect to the CentOS system via SSH and try logging in as root.  The attempt should be denied even if the password is correct, which means that it is working.

## Technical Terms

### SSH
For more information about Secure SHell (SSH), see the Tech Terms entry "SSH" in [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md).

### CentOS
CentOS is a distribution of the open source operating system "Linux".  It is closely related to the company Red Hat, which provides Linux service and support.  As such, it is a common version used in enterprise settings.

For more information about CentOS, try [this](https://www.centos.org/) resource.
*CentOS, "The CentOS Project".  Date Not provided*

### /etc/passwd and uid's
The /etc/passwd file in most Linux operating systems is a file that contains data about users and user accounts, such as their names, user and group id's, and home directories, among other things.  Note that passwords are no longer stored here as a result of security and encryption changes, and were instead moved to the /etc/shadow file.

For more information about the /etc/passwd file, try [this](https://www.cyberciti.biz/faq/understanding-etcpasswd-file-format/) resource.
*Gite, Vivek, "Understanding /etc/passwd File Format".  December 2nd, 2019*

### /etc/ssh/sshd_config
In the Linux operating system, nearly everything, especially system and service configurations, is stored in simple files.  The file to configure the SSH service, called sshd_config, is found in the /etc/ssh file, and can be edited using sudo.  Many of the lines are commented out until the user decides to change or implement certain features, and they can do so simply by uncommenting and typing in the line with a text editor.

For information about how to block the root user from SSH access on CentOS, try [this](https://www.tecmint.com/disable-ssh-root-login-in-linux/) resource.
*Cezar, Matei, "How to Disable SSH Root Login in Linux".  December 16th, 2017.*
