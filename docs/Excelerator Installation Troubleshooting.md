---
title: Excelerator Installation Troubleshooting
tags:
- Support
- Excelerator
- Installation
description: Installation From Summer 2019 all Excelerator client installations were
  rewritten and made per-user. (Per-user installations only affect the single…
created: '2019-12-03'
modified: '2023-09-12'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Client%20Installation%20and%20Setup%20Guide.aspx
---

# Installation

From Summer 2019 all Excelerator client installations were rewritten and made per\-user.   (Per\-user installations only affect the single user making the installation.)

Installers are provided in either msi or exe format.  These can be downloaded from our website.  

- The exe provides a slightly more user\-friendly experience, automatically creates a log and the possibility of easily running as an Administrator.
- The msi can be used for administrative installs (see below) and this format is required for some software distribution technologies.

Basic per\-user installations should be carried out when logged in as the Excelerator user not as Administrator.  Double\-click the exe installer.  The installation path can be changed by clicking on the "Options" button.   Read the End User Licence Agreement and accept if you agree with it.  

If the installation seems to complete successfully, then open Excel and check the "Excelerator" ribbon tab appears.

![ExceleratorTab.png](images/PublishingImages_Pages_Excelerator_Client_Installation_and_Setup_Guide_ExceleratorTab.png) 

# Background

Excelerator appears in the ribbon tab because it is an Excel Addin ([https://docs.microsoft.com/en\-us/office/dev/add\-ins/excel/excel\-add\-ins\-overview](https://docs.microsoft.com/en-us/office/dev/add-ins/excel/excel-add-ins-overview)).  Excel addins load using a 3rd party component Addin Express.  See [Excelerator Installation \- adxloader.aspx](Excelerator Installation - adxloader.md).  For the ribbon to appear the addin express part has to load, and then the Excelerator assemblies have to load.  

# What Does the Installer Do?

It does two things:

- Copy some files onto the PC
- Register the add\-in in Excel that gets the ribbon to display.

## Files

In a per\-user installation, there are no longer any changes to central files or registry locations.  Only per\-user locations are updated

Files (mostly assemblies) are installed to %localappdata%\\Codis Limited\\\<app name\> folder

## Add\-in Registration

The installer runs a command ADXRegistrator that attempts to register the Add\-in.  Addin registration consists of updates to the Windows registry.   

Registry updates are made to HKCU area.  The registry updates are described in detail in Addin Express developers guide: [adxnet.pdf](https://codislimited.sharepoint.com/sites/Wiki/Development/adxnet.pdf) starting page 206\.    

# Logging

There are two types of logs.  Logs that are updated during the installation and logs that are updated when the software attempts to run.  

## Installation Logs

Logs can provide helpful information in the event of an installation failing.  There are 2 logs that can be updated in a complete Excelerator installation.   

- Installer log
- ADX Registrator Log

### Installer Log

This is created by the installation MSI or EXE.  The EXE install always create a log and provides a link to it.  The MSI install has to be told to create the log.  

#### EXE Installation

The exe installation is logged by default, and a link to the log is shown at the end of the installation.  The log files are created in the %TEMP% folder.  Two files are created \- one for the bundle and one for the package within the bundle.  Both are named after the installer e.g. "Codis Sage 1000 Release Standard Excelerator\_20191207101256\_000\_ExceleratorSetup.log".  The package one (with "ExceleratorSetup") in its name is likely to contain the diagnostic information needed.  

#### MSI Installation

Run the command:  

### ADX Registrator Log

This is created in the %TEMP%\\\<Product Name Tag\> folder.    

The product name tag could be e.g. "Codis\_Excelerator\_Sage200\_SharedAddin"

## Runtime Logs

These are logs that are updated every time Excelerator attempts to load (although the registration has to be successful for this to happen).  

### Adxloader log

This is also created in the %TEMP%\\\<Product Name Tag\> folder.  It records the Addin express addin attempt to load.    

adxloader.log does not seem to always be populated.  

### Excelerator Log

This log can be found in %userprofile%\\AppData\\Roaming\\Codis\\Excelerator

The Excelerator program updates this log once the add\-in loads the program.   Its output is in XML format and can be viewed using the Log Viewer option in Excelerator.  The output format can be configured in the Codis.Excelerator.Sage200\.Standard.Addin.dll.config file.

It contains details about which modules are detected and loaded.  If the Excelerator log is updated, it shows that the add\-in has successfully loaded the Excelerator program.

The Log Viewer program is available in the installation folder as a stand\-alone program.  

# Installation Troubleshooting

See also: [Online Licensing Troubleshooting.aspx](Online Licensing Troubleshooting.md)  

## Error: User Installations are not allowed

This message is displayed during installation:

"*The system administrator has set policies to prevent this installation*." (msi install)

 "*This installation is forbidden by system policy*" (exe installation)

The following message is found in the log: "*Machine policy value 'DisableMsi' is 1*"

This means that the system administrator has disabled User installations.  There are two possible solutions:

1. Make the user part of the administrators group then run as administrator.  Do not run as administrator if the user does not have administrator rights as the installation will appear successful but it will install to the administrator user.
2. An administrator makes an *administrative installation* (see below) then the user installs from this.

## Error:This installation is forbidden by system policy. Contact your system administrator.

Check *Computer Configuration \> Administrative Templates \> Windows Components \> Windows Installer* for a DisableMSI setting.  There might not even be a Windows Installer subkey.  

Run gpedit and check settings in *Computer Configuration\-\>Administrative Templates\-\>Windows Components\-\>Windows Installer*  

Try this.  May work without the reboot  

- Click Start \-\> Control Panel
- Open Administrative Tools
- Open Local Security Settings
- Click Software Restriction Policies
	1. If no software restrictions are defined, right\-click the Software Restriction Policies node and select New Software Restriction Policy
- Double click Enforcement
- Select "All users except local administrators"
- Click OK
- Reboot the machine
### Installation appears to be successful, but the toolbar does not appear

This can be because the add\-in did not register.  Check the adxregistrator.log (see above).  It might indicate that the registry update was unsuccessful and which key or keys failed to update.   Usually, the problem is permissions.  Check the registry HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\Excel\\Addins. There should be an entry for the product e.g. Codis\_Excelerator\_Sage200\_SharedAddin.AddinModule.    
![ExceleratorRegistryEntry.png](images/PublishingImages_Pages_Excelerator_Client_Installation_and_Setup_Guide_ExceleratorRegistryEntry.png)  

This should have entries like these below the product subkey (e.g. Codis\_Excelerator\_Sage200\_SharedAddin.AddinModule), :  

![ExceleratorRegistryDetails.png](images/PublishingImages_Pages_Excelerator_Client_Installation_and_Setup_Guide_ExceleratorRegistryDetails.png)  

If the entry for the product or the entries below are missing then it will probably due to permissions on the registry.  Sometimes the Addin registry hive has special permissions that allow the product entry to be created but does not assign write permissions to product subkey  so the sub keys and the entries shown above are not created.  

This video shows an example of permissions that prevent Excelerator from registering properly and how changing those permissions allow it to register.  Bear in mind that the restrictive permissions might be a result of a deliberate attempt to prevent office addins from being installed.  It may result from a group policy but we've not been able to identify it yet.  

Sometimes, the add\-in can register but not correctly, or system policies prevent the add\-in from running.  Check if the Add\-in appears in Excel and its attributes: In Excel Check File\-\>Options\-\>Add\-Ins in Excel.  

### Message: The Add\-in you have selected is disabled by your system administrator

![AddinSelectedDisabled.png](images/PublishingImages_Pages_Excelerator_Client_Installation_and_Setup_Guide_AddinSelectedDisabled.png)  

This may be caused by a system policy.  See : [https://getadmx.com/?Category\=Office2016\&Policy\=excel16\.Office.Microsoft.Policies.Windows::L\_BlockAllUnmanagedAddins](https://getadmx.com/?Category=Office2016&Policy=excel16.Office.Microsoft.Policies.Windows::L_BlockAllUnmanagedAddins)  

## Addin Appears to Register But Still Does Not Appear in Excel

If it appears in the COMs addin list and isn't ticked, then tick it.  If it doesn't appear, try using the Add button to add it by entering a path to the adxloader.dll file in the installation folder.  

## Error creating object with name 'SageApplication'

This can only happen with Sage 200\.  

"Error creating object with name 'SageApplication' defined in 'assembly \[Codis.Sage200, Version\=3\.2\.90\.0, Culture\=neutral, PublicKeyToken\=aacfe802eb9097a4], resource \[Codis.Sage200\.SageApplicationObjectConfiguration.xml] line 7' : Initialization of object failed : Cannot instantiate Type \[Codis.Sage200\.Core.SageApplication] using ctor \[Void .ctor()] : 'Could not load file or assembly 'Sage.Accounting.Financials, Version\=19\.0\.0\.0, Culture\=neutral, PublicKeyToken\=56cc4aa2c6a12364' or one of its dependencies. The system cannot find the file specified.'"  
Somehow it is trying to load the wrong version of Sage.Accounting.Financials or is finding the wrong version.  See [Sage 200 Excelerator Assembly Resolution.aspx](Sage 200 Excelerator Assembly Resolution.md)  

Try searching the PC for other versions of the Sage.MMS.SAA.Client.dll assembly.  

## Administrative Installations

There are two scenarios where we can suggest the administrative installations. You need to be an administrator and must use the excelerator msi installer setup file for both scenarios.  

### **Scenario 1** \- Where the users are restricted to do excelerator installation.

An administrative install command creates an installation image in a folder (typically a shared network folder).  Users can then install the software from their profiles by double clicking the msi created by this command.   The administrative install command is  

**msiexe /a \<msi source path\>**  

**Note: Destination Path should not be the same as Source Path.**

**Command for Silent/Quite Install with install log: \-** msiexec /a \<Source Path\> TargetDir\=\<Destination Path\> /qn /l\*v install.log  

![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_1.jpg)  

![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_2.jpg)  

Select the common folder to extract to \- it should be a shared network folder that the users who need to install the software can access for Scenario 1 but can be a normal folder for Scenario 2\.  A new msi with the same name as the one you've just used will be created in this common folder along with the Codis Excelerator Application Folder.  

![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_3.jpg)![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_4.jpg)![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_5.jpg)  

The user should double\-click on this new msi to install the software.  The installation should no longer be stopped due to "User installation not being allowed". An UAC prompt may be displayed for administrator credentials, but it would not install to the administrator's profile.  

![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_6.jpg)  

### **Scenario 2** \- Where the customer wants to install Excelerator in a common central folder on a Remote Desktop Server (RDS) environment for all remote desktop users.

Once the Codis Excelerator Application folder is extracted in a common folder (Codis) on RDS server through the above administrative install command as shown in Scenario 1, then use the ADXRegister.BAT file in this extracted folder (Codis Limited \-\-\> Sage 200 Excelerator) to register the Excelerator addin for each excelerator user. You may keep or discard/delete the .msi created in this common folder which is not required for this scenario.

Then please go ahead with the licencing process for 1 user. This will generate LicenceData folder inside the extracted Codis Excelerator folder as shown below.

All excelerator domain users will need to have full access permission on this LicenceData folder. We suggest adding Sage 200 users and Sage 200 admins group to it and give full access permission.  

![](images/Support_Support_Wiki_Images_Excelerator_Administrative_Install_7.jpg)  

When the other users will refresh the licence from their profiles, we will get their respective end devices on our licencing system and based on their excelerator module access we will tick their end devices or the customer can send us the respective end user's device (PC) names to us before hand and their respective module access and we will get that ready. The excelerator users would just need to refresh the licence once from their profiles.  

[https://docs.microsoft.com/en\-us/windows/win32/msi/administrative\-installation](https://docs.microsoft.com/en-us/windows/win32/msi/administrative-installation)  

## Policies influencing installations

[https://docs.microsoft.com/en\-us/windows/win32/msi/machine\-policies](https://docs.microsoft.com/en-us/windows/win32/msi/machine-policies)
