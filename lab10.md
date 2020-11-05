# Lab 10 - Powershell Scripting

## Points of interest

### PowerShell PSRemoting commands

https://docs.microsoft.com/en-us/powershell/scripting/learn/remoting/running-remote-commands?view=powershell-7
https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-7


### AD from the command line

 - users
 - groups
 - Get-Command New* -Module ActiveDirectory

https://www.pdq.com/blog/add-users-to-ad-with-powershell/
https://community.spiceworks.com/how_to/50409-add-ad-user-to-groups-with-powershell

## Technical Terms

### Powershell syntax
PowerShell is essentially a command shell constructed with an object-oriented programming language built directly into the kernel.  This allows for attribute access and manipulation across all sorts of data points in a system.  Most PowerShell commands (save short and aliased commands) fit the syntax ```Verb-Noun```, such as ```Write-Host```, specifying an action and what to use it on.  Similar to other shells, many commands will take parameters, either passed directly, piped, or in variable form, where variables are denoted with the common dollar sign ($) symbol.  options are typically denoted with a dash (-), and can be used to directly reference the variable to which they will correspond as the parameters to the command script, such as -Type.  Note that in using PowerShell, "commands" are typically referred to as "command-lets", or "cmdlets".

For more information about PowerShell syntax, try [this](https://ss64.com/ps/syntax.html) resource.
*SS64, "Windows PowerShell How-to guides and examples".  Date not provided*

### Powershell scripting

#### loops

#### parameters
https://stackoverflow.com/questions/52170699/how-to-save-each-line-of-text-file-as-array-through-powershell

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

```Invoke-Command -ComputerName <name> -ScriptBlock { <command> }```
Allows the user to run a specified command as a different computer, given after the -ComputerName option