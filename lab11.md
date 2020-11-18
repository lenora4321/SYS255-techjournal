# Lab 11 - Automation

## Points of interest

### Configuration of clone boxes
The three Linux boxes in this lab were configured similar to the initial configuration detailed in [lab 3](https://github.com/lenora4321/SYS255-techjournal/blob/master/lab3.md).  Each was assigned a static IP address with corresponding gateway, DNS, and search domains, as well as a hostname.  The specific names and IP addresses are detailed below:
 
 - 10.0.5.70 (hostname: clone1)
 - 10.0.5.71 (hostname: clone2)
 - 10.0.5.72 (hostname: clone3)

Each of the systems was also modified so that escalation to root could be done without password, given that the logged-in user was a member of the wheel group.  To do this, the ```/etc/sudoers``` file was altered slightly (read comments in said file for more details).  Each system was also given a single named user, "lenora", which was added to the wheel group.  Note that these systems, though connected to the LAN, were not joined to the active directory using realmd.

### RSA key creation
To allow for more secure and robust authentication between the clone machines, clone1 was used as the controller and generated asymmetric SSH keys to be shared with the other two clones.  To do this, ```ssh-keygen``` and ```ssh-copy-id``` were used (as detailed in the commands section) so that the public key was copied to the .ssh/ directory of clone2 and clone3, while the private key remained on clone1.  After this, the latter clones could be connected to via SSH without provideing a password, just the passphrase used for the key.

To streamline the process even more, the ```ssh-agent``` was used to cache the passphrase between two connected systems for a set time of one hour, by utilizing the ```ssh-add``` command as detailed in the commands section below.

### Automation
Throughout this lab, both pssh and ansible were used to automate a number of simple test functions on clone2 and clone3.  For more details about either method, see their respective entires in the sections below.

Ansible was used to automate:
 - ping
 - adding port 8080 to firewall
 - install nginx and create a test file to curl from

PSSH was used to automate:
 - uptime
 - uname -a
 - installation and running of ```tree```

## Technical Terms

### Encryption
Encryption is a way of encoding and decoding data using reversible mathematical computations, in order to ensure, among other things, confidentiality and integrity.  One of the first methods of encryption was the Caesar Cipher, a method of shifting letters in a message to encode them, and shifting them back to reveal the message.  Today, we use much more advanced methods to encrypt data, including special "keys" that allow for the decryption of the data for those who possess them.  Below are outlined two of the umbrella types of encryption, as well as a few modern algorithms that implement them.

#### Symmetric
Symmetric (meaning "same") encryption is a type of encryption that uses the same key to encode and to decode the data.  En example of this would be having the same house key to lock and unlock a home.  Provided that the keys are in the hands of the correct people, this means that only those who have the keys can get to the data within the "house".  A concern in using symmetric encryption is often the distribution of the key.  If a key gets into the wrong hands when being given out to the authorized users, the individual with the key essentially has the same access as those who should have it.  Symmetric keys are often less computationally expensive than asymmetric keys, which is often touted as one of its high points.  Today, when symmetric encryption is used, distribution is often handled by an asymmetric algorithm, so that the expensive encryption can be used to ensure the keys are in the right hands, before using the faster, more efficient encryption for the rest of the conversation.  TLS today uses this method to secure its conversations.

Some examples of symmetric encryption algorithms are:
 - AES
 - IDEA
 - RC5
 - Blowfish

#### Asymmetric
Asymmetric encryption uses a pair of mathematically related keys, one to encrypt data and the other to decrypt it.  Encryption is typically done via a "public key", which anyone can have, so that distribution is not an issue.  Once encrypted, the data can then only be decrypted by the person holding the "private key", which is never distributed.  In order to ensure identity, asymmetric key pairs are often used in pairs themselves, with each side having one public and one private key, which correspond to the private and public keys of the other entity, respectively.  In this way, when one side sends public-key encrypted data, they can sign it with their private key to verify that it was them.  Once the receiving entity verifies the private key, they can decode the data with their own private key.  This method is more secure than symmetric-key encryption because distribution is much less an issue; however, the algorithms used to create and operate asymmetric keys are more computationally expensive than those used for symmetric keys.  Because of this, asymmetric keys are often used to distribute symmetric keys, so that the data can get the security bonus of asymmetric encryption with the performance bonus of symmetric encryption.

Some examples of asymmetric encryption algorithms are:
 - Diffie-Hellman
 - RSA
 - DSA

For more information about symmetric and asymmetric encryption, try [this](https://blog.keyfactor.com/symmetric-vs-asymmetric-encryption) resource.
*Ryan Yackel, "When to Use Symmetric Encryption vs. Asymmetric Encryption".  Key Factor Blog, June 17, 2020*

### Ansible
Ansible is a tool/API used to automate command  execution across multiple remote systems.  It can be installed on Linux via yum and the module name.  Details of the options used can be found in the commands section below.  One thing unique to ansible is the concept of a "playbook", which is a simple text file that is provided to the ```ansible``` command.  This file provides at least two things:

 - the hosts to run on
 - one or more commands to run

The file used is organized using YAML syntax, which is similar to JSON or XML, except that it appears more human-readable.

For more information about andsible and playbooks, try [this](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html#playbooks-intro) resource, as well as the surrounding website.
*Ansible, "Intro to playbooks".  Red Hat, Inc, Nov 5, 2020.*

 
### PSSH
Parallel Secure SHell command.  This allows for commands to be run on one device and carried over to others at the same time, with just a single command.  This method is great for automation, since it removes the necesity to log in to each system and run commands *n* number of times for *n* number of systems.  There are good examples found in the man pages of linux system for this.  In order to install this command, install ```epel-release``` **and then** ```pssh``` via ```yum```.

For convenience, a few sample commands can be found here.  Note that for the ```hosts.txt``` file, the contents are simply the host names, each on a new line, but could entail the user@system, ports, and IP addresses as well.

 - ```pssh -i -H "host1 host2" echo "hello world!"```
 - ```pssh -i -h hosts.txt echo "hello world!"```

For more information on pssh, try the man pages of any linux system, or try [this](https://www.tecmint.com/execute-commands-on-multiple-linux-servers-using-pssh/) resource.
*Aaron Kili, "Pssh – Execute Commands on Multiple Remote Linux Servers Using Single Terminal".  TechMint, December 5, 2015*

## Commands

```firewall-cmd --add-port=8080/tcp``` allow traffic to tcp port 8080 to come through firewall.  Use ```--permanent``` to maek it stay through reboot.  For references on this command, try [this](https://www.cyberciti.biz/faq/how-to-open-firewall-port-on-ubuntu-linux-12-04-14-04-lts/) or [this](https://docs.bitnami.com/virtual-machine/faq/administration/use-firewall/) resource.

*Vivek Gite, "How To Ubuntu Linux Firewall Open Port Command". CyberCiti, May 17, 2020*
*"Open Or Close Server Ports".  Bitnami Documentation, date not provided*

```ansible``` Command API used to create and run a "playbook" of commands against a set of hosts simultaneously.  Include word *all* after initial command, most likely to run on all provided hosts
 - **-i** "inventory"; specify a list of hosts separated by commas **or** a file where the hosts are stored
 - **-m** module name to execute; by default, this is just the name of a command, ex: "-m ping"
 - **-b** execute module as sudo
 - **-a** "module arguments"; can take a string command name to run on multiple hosts.  Can be used similar to -m in this context

```ssh-add``` Used to allow secure passphrase ssh with keys, but will cache the passphrase so that it need only be entered once.
 - **-t <1h>** time option; cache the passphrase for 1hour

```ssh-keygen``` Generate an RSA key pair for SSH connection.  This key can then be shared to the remote systems with the ```ssh-copy``` command, as outlined below.  Will ask for a file location for the resultant key and for a passphrase to use to secure the key.  By default, the keys will be stored in the home directory in a ```.ssh``` directory

```ssh-copy-id <user@system>``` Copy an ssh key to a remote machine.  The resultant key should be stored within ```.ssh/authorized_keys```.  Will prompt for a passphrase among other things; passphrase is a very good idea as it will provide an extra level of security.

 - **-a** do on all ssh-connected hosts

```pssh```
Parallel ssh command.  Run commands on multiple systems at once via ssh.

 - **-i** inline; allows for standard error and output to be displayed for each host as normal
 - **-H <"space-separated hosts in quotes">** specify the hosts to run the subsequent command on
 - **-h <filename>** specify a file containing the hostnames to run the subsequent command on
 