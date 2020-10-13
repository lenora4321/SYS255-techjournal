# Lab 7 - Server Core and Remote Administrator Tools

## Points of interest

### Configuration via sconfig tool

### File Service Tools

 - adding features
 - adding server
 - files server resource manager
### OU structure

### S:\ drive map
 - create GPO under SYS255
 - ensure that Authenticated users is in the security filtering
 - edit
 - user config
 - prefernces
 - windows settings
 - drive maps
 - create new
 - create
 - location \\fs01-lenora\Sales
 - use S
 - show this and all drives
 - common:
	- run in logged-on user's security context
	- item-level targeting > targeting > remove/add so that only security group is included > add sales-users

 [this](https://activedirectorypro.com/map-network-drives-with-group-policy/) resource.
 [this](https://blogs.manageengine.com/active-directory/active-directory-academy/2019/11/18/mapping-drives-using-group-policy-preferences.html)
 [this](https://www.faqforge.com/windows/map-shared-folder-network-drive-using-group-policy/)
 
 

## Technical Terms

### Windows Server Core

### File Server

### Windows permissions:

 - NFTS
 - Share
 
### Universal Naming Convention (UNC)

## Commands

```sconfig```

```\\fs01-lenora\sales```




