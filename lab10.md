# Lab 10 - PowerShell Scripting

## Points of interest

### PowerShell PSRemoting commands
PSRemoting allows for commands to be run remotely on one or more computers.  This may be blocked by the firewall by default.  For this lab, the assignment was to connect successfully to an interactive remote session or to get any of the other PSRemoting commands to function.  The firewall did not interfere in this case, so the command was simply run and a remote session entered.  See the "Commands" section for details.

For more information about PSRemoting, try [this](https://docs.microsoft.com/en-us/powershell/scripting/learn/remoting/running-remote-commands?view=powershell-7) resource.
*Microsoft Docs, "Running Remote Commands".  Microsoft, date not provided*

For help letting PSSession through the firewall, try [this](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-7) resource.
*Microsoft Docs, "Enable-PSRemoting".  Microsoft, date not provided*

### AD from the command line

 - users
 - groups
 - Get-Command New* -Module ActiveDirectory

https://www.pdq.com/blog/add-users-to-ad-with-powershell/
https://community.spiceworks.com/how_to/50409-add-ad-user-to-groups-with-powershell

## Technical Terms

### PowerShell syntax
PowerShell is essentially a command shell constructed with an object-oriented programming language built directly into the kernel.  This allows for attribute access and manipulation across all sorts of data points in a system.  Most PowerShell commands (save short and aliased commands) fit the syntax ```Verb-Noun```, such as ```Write-Host```, specifying an action and what to use it on.  Similar to other shells, many commands will take parameters, either passed directly, piped, or in variable form, where variables are denoted with the common dollar sign ($) symbol.  options are typically denoted with a dash (-), and can be used to directly reference the variable to which they will correspond as the parameters to the command script, such as -Type.  Note that in using PowerShell, "commands" are typically referred to as "command-lets", or "cmdlets".

For more information about PowerShell syntax, try [this](https://ss64.com/ps/syntax.html) resource.
*SS64, "Windows PowerShell How-to guides and examples".  Date not provided*

### PowerShell scripting
Similar to bash and other shell scripting, scripting for PowerShell can be done by entering a group of commands into a shell file and running it as an executable.  The commands for running a shell file as an executable in PS are listed in the Commands section below.  The file type used in shell scripting for PS is a .ps1 file.  When invoked as an executable script, such a file can take in parameters, parse objects, write to console and file, and do a number of other common shell script functions, except in a more object-oriented way.  Commands can be separated by semicolons (;), and piping (|) works here as in bash scripting.

For a basic tutorial on more PowerShell scripting features, try [this](https://blog.netwrix.com/2018/02/21/windows-powershell-scripting-tutorial-for-beginners/) resource.
*Skur, Ian, "Windows PowerShell Scripting Tutorial for Beginners".  Netwrix Blog, February 21, 2018*

#### loops
Loops in PowerShell are typically done as a classic programming for-each loop.  The syntax for a for-each loop in PS is the keyword ```foreach``` followed by a set of parentheses containing the name of the new reference variable and the collection of things to loop through.  The list of commands to run for each element in the loop is then contained within a pair of curly braces ({}).  Several examples of this are included below:

 - ```foreach($name in $nameArray) { Write-Host $name }```
 - ```foreach($item in $myPath.split(':')) { Write-Host $item }```
 
In theory, a loop could most likely be done iteratively as well, but this is not so typical in shell scripting, where collections of objects are passed around in variables, typically as output from a command.

#### parameters
Parameters, also known as "arguments", can also be passed to a PS script, just as in bash.  These are passed usually as the first few lines of a shell script.  They can be directly denoted as what they are referencing by the referring to the name of the variable in the options when the command is invoked, followed by the desired value.  The ```param``` identifier in the script is then used to assign the given values to variables, denoted \[type\] $varname within the parentheses of the ```param``` function.  An example of this is shown below.

 - Command: ```PS C:\> .\shellScript.ps1 -name "Edward Elric"```
 - Script: ```param([string] $name) ; Write-Host $name```

For help trouble shooting lists of data and parsing them as string, try [this](https://stackoverflow.com/questions/52170699/how-to-save-each-line-of-text-file-as-array-through-powershell) resource.
*Bevan, John L, "How to save each line of text file as array through powershell".  StackOverflow, September 4, 2018*

## Commands

```New-Item```
Similar to ```touch``` in Linux.  Allows for the creation of new items, specifically new files, as used in this lab.

```Write-Host <stringVal or $variable>```
Similar to the ```echo``` command in Linux.  Write a string or the contents of a variable out to the host screen.

```Set-Alias -Name <name> -Value <CommandToAlias>```
Allows the user to create an alias for a specific command.  This can be helpful either for saving longer commands to a shorter prefix, or can be used to alias commands to names that other shells (such as Bash) might use.  To see all aliases a shell is aware of, run ```alias```.

```Set-ExecutionPolicy -Scope CurrentUser RemoteSigned```
Allows for files to be run as executables by the current user.  Similar to ```chmod +x``` in Linux.  May require Administrator permissions within PowerShell.

```Resolve-DnsName <hostname> -Type <record type>```
Functions similar to nslookup, but with more DNS record data; returns an object that can be parsed with PowerShell commands.  The DNS record type, such as "A" or "ptr" can be specified after the -Type option.

```Select-Object```
Take piped input and select certain attributes of the object, which can the be themselves piped out or simply printed to console.

```Enter-PSSession --ComputerName```
Enter an interactive command prompt to a remote PowerShell instance on another computer.  Results are displayed locally.

```Invoke-Command -ComputerName <name> -ScriptBlock { <command> }```
Allows the user to run a specified command as a different computer, given after the -ComputerName option