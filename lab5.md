# Lab 5 - ADDS and Group Policy

## Points of interest

### Creation of OUs, Users, and Groups
In the Active Directory Users and Computers panel opened up from the Server Manager, one organizational unit was added directly under the domain, by the name of "SYS255".  Sub-OUs were then added by the names of "Accounts", "Computers", and "Groups".  The lists below give a basic overview of the users, groups, and computers added to each organizational unit.  Note that some of the objects were created, and others moved from previous locations, specified below.

**Accounts** Three new users were added to the accounts OU, each with the name listed below.
 - User alice
 - User bob
 - User charlie

**Computers** Only one computer was added to the computers OU.  This device was the Workstation from previous labs and was moved from the domain computers folder to this OU.
 - WKS01-Lenora

**Group** One group was created and added to the groups OU.  The purpose of this group was to hold users that could then have settings applied to them regarding their desktop display.  Two of the three new users, alice and bob, were added to this group.
 - custom-desktop

### Group Policy configuration
To add actual settings, called in sum a "policy", the Group Policy Management panel was opened from Server Manager.  A group policy object was then added to the SYS255 OU and set to contain only the new custom-desktop group and domain computers (authenticated users was removed).  The last step before actual policy addition was to deny domain users from applying the group policy.

#### User policy - recycle bin removal

#### Computer policy - last login data removal

## Technical Terms

### Object
An object, in terms of the Windows Active Directory, is any unit that can have settings applied to it.  This can potentially include groups, contacts, and other things, though it is mostly used to reffer to computers and users.

 - Computers: the physical/virtual devices that are connected under one domain.  Settings for this are applied at boot time and can include valid logon accounts and connection settings, among other things.
 - Users: the users/accounts that are connected to one domain.  Settings for this are applied at logon and can include, among other things, desktop settings, file access, and other permissions.
 
For more information on types of domain objects, try [this](https://www.windows-active-directory.com/active-directory-objects.html) resource.
*Active Directory 360, "Active Direcotry Objects".  Date not provided.*

### Organizational Unit (vs folders)
Organizational units are similar to directories/folders in that they can be used to contain and organize objects (see entry above for object description).  The difference is that organizational units can have the capacity to have settings applied to themm in the form of group policies, which can be configured to go beyond the default domain policy.  For example, an OU holding a set of users might give those users access to certain files that the base domain gives access to.  An OU holding a set of computers might restrict the various users which can log in from it.

For more information about Organization Units, try [this](https://kb.iu.edu/d/atvu#:~:text=An%20organizational%20unit%20(OU)%20is,organization's%20functional%20or%20business%20structure.) resource.
*Knowledge Base, "About organizational units in Active Directory".  Indiana University, October 7, 2019*

### Group Policy Object
A group policy object is a collection of settings that can be applied to an Organizational Unit.  It must have a unique name, and is created by a domain administrator using a Group Policy editor (see commands and sources below).

For more information about GPOs, try [this](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/policy/group-policy-objects) resource.
*Microsoft Docs, "Group Policy Objects".  May 31, 2018.*

For a brief overview of the Group Policy Editor, try [this](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/policy/group-policy-object-editor) resource.
*Microsoft Docs, "Group Policy Editor Object".  May 31, 2018*

### SAM account
SAM Stands for Security Account Manager.  It is a database that is used to store local user and group accounts, and properly allows for authenticated login.  It is typically associated with a long ID that serves as the unique identifier for devices and accounts.
 - SID: this is the ID number stored in conjunction with a name and serves as the unique identifier for an object.
 - Account name: this is the human-readable name that is associated with an SID.  Note that this can be changed and may not reflect what the actual status of the account is; for example, "administrator" is a term that implies ultimate power, but may actually just be the name.  See the SID for a more accurate reflection of account status.
A sample ID/name combo may look like this: Name: Administrator		SID: S-1-5-21-3830937358-1556556057-988213067-500

For more information on SAM Accounts and SIDs, try [this](https://www.windows-active-directory.com/windows-security-account-manager.html) resource.
*Active Directory 360, "Security Account Manager".  Date not provided.*

## Commands

```gpresult```
"Group polict result, resultant set of policies".  Shows the set of group policy settings applied to the remote user/computer, specified by SAM name.

**/r** Displays RSoP summary data (overview).

**/scope** Takes either "user" or "computer" as parameters, displays only the RSoP for one or the other specified.

For more information about gpresult and its options, try [this](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/gpresult) resource.
*Ross, Elizabeth, et al.  "gpresult".  Microsoft Docs, October 16, 2017*

```gpedit```
"Group policy edit".  Edit the group policy settings on the local computer/user.  Not available for anything less than Windows 10 Pro versions.

```gpupdate```
"Group policy update".  Updated the group policies on a machine so that the settings are up to date with the active directory.

**/force** Forces the updates when the command is run instead of waiting until an optimal time.



