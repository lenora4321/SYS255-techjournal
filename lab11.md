# Lab 11 - Automation

## Points of interest

### Configuration of clone boxes

 - edit of ```/etc/sudoers``` to allow escalation to root without password for those within wheel

### RSA key creation

### Automation

## Technical Terms

### Encryption

#### Asymmetric

#### Symmetric

### Ansible

 - Playbooks
 
### PSSH
Parallel Secure SHell command.  This allows for commands to be run on one device and carried over to others at the same time, with just a single command.  This method is great for automation, since it removes the necesity to log in to each system and run commands *n* number of times for *n* number of systems.  There are good examples found in the man pages of linux system for this.  In order to install this command, install ```epel-release``` **and then** ```pssh``` via ```yum```.

For convenience, a few sample commands can be found here.  Note that for the ```hosts.txt``` file, the contents are simply the host names, each on a new line, but could entail the user@system, ports, and IP addresses as well.

 - ```pssh -i -H "host1 host2" echo "hello world!"```
 - ```pssh -i -h hosts.txt echo "hello world!"```

For more information on pssh, try the man pages of any linux system, or try [this](https://www.tecmint.com/execute-commands-on-multiple-linux-servers-using-pssh/) resource.
*Aaron Kili, "Pssh – Execute Commands on Multiple Remote Linux Servers Using Single Terminal".  TechMint, December 5, 2015*

## Commands

```firewall-cmd --add-port=8080/tcp``` allow traffic to tcp port 8080 to come through firewall.  Use ```--permanent``` to maek it stay through reboot.  For references on this command, try [this](https://www.cyberciti.biz/faq/how-to-open-firewall-port-on-ubuntu-linux-12-04-14-04-lts/) or [this](https://docs.bitnami.com/virtual-machine/faq/administration/use-firewall/) reousrce.

*Vivek Gite, "How To Ubuntu Linux Firewall Open Port Command". CyberCiti, May 17, 2020*
*"Open Or Close Server Ports".  Bitnami Documentation, date not provided*

```ansible```

```ssh-add``` Used to allow secure passphrase ssh with keys, but will cache the passphrase so that it need only be entered once.
 - **-t <1h>** time option; cache the passphrase for 1hour

```ssh-agent```

```ssh-keygen```

```pssh-hosts```

```ssh-copy-id <user@system>``` Copy an ssh key to a remote machine.  The resultant key should be stored within ```.ssh/authorized_keys```.  Will prompt for a passphrase among other things; passphrase is a very good idea as it will provide an extra level of security.

 - **-a** do on all ssh-connected hosts

```PSSH```
Parallel ssh command.  Run commands on multiple systems at once via ssh.

 - **-i** inline; allows for standard error and output to be displayed for each host as normal
 - **-H <"space-separated hosts in quotes">** specify the hosts to run the subsequent command on
 - **-h <filename>** specify a file containing the hostnames to run the subsequent command on
 