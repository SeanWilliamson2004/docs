---
title: Sage 1000 V1 and V3 Release Procedures
tags:
- Support
- Excelerator
- Release
description: Deprecated Procedure for new Excelerator Release These are the steps
  to be followed when issuing a new release of Excelerator V3 modules Release of…
created: '2017-01-27'
modified: '2020-05-07'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%201000%20V1%20and%20V3%20Release%20Procedures%20-%20Deprecated.aspx
---

**Deprecated**

**Procedure for new Excelerator Release** These are the steps to be followed when issuing a new release of Excelerator V3 modules 

## Release of Excelerators

  
The programs for Enterprise and Standard are still different but the templates are the same, unlike in previous versions. 

### Testing

When starting a test cycle, take copies of the files in the pre\-release folder and place them in a new folder with the date of the start of testing.   
eg. TESTING Release27\-07\-2015 For example:\-   
[\\\\CD01SR16104\\Testing\\Sage1000Testing](file://///cd01sr16104/Testing/Sage1000Testing)  TESTING Release12\-07\-2015 If testing restarts after fixes then keep this folder up to date with the latest version being tested. When the release is done rename this folder to the date of the release eg. TESTED Release 10\-08\-2015\. Separate folders for Standard and Enterprise are maintained. Sage 500/1000 Excelerators are in :\-   
Standard setups V1 are in :\- [\\\\CD01SR16104\\PrereleaseFolder](file://///cd01sr16104/PrereleaseFolder) USE THE .ZIP files with version number on as the named folders are out of date. 

Standard setups V3 are in :\- [\\\\CD01SR16104\\PrereleaseFolder\\StandardExceleratorsNET](file://///cd01sr16104/PrereleaseFolder/StandardExceleratorsNET)

Enterprise setups:\- [\\\\cd01sr16104\\PrereleaseFolder\\Enterprise Setups](file://///cd01sr16104/PrereleaseFolder/Enterprise%20Setups). There are sub folders for V1 and V3 

### Deployment

See [ALM \- Excelerator Release to Customers Deployment](ALM - Excelerator Release to Customers Deployment.md)

## Releasing

The files highlighted in the screenshot above, were in pre\-release at the start of the test cycle but were not ready to be tested so they will be removed from this test folder and not copied to the release folder. The network address of the release folder is:\- [\\\\192\.168\.3\.212\\Release\\Sage\_1000\_Standard\_V3](file://///192.168.3.212/Release/Sage_1000_Standard_V3) 

The following is the front end address for information only. 

[ftp://codisftp.codis.co.uk/Release/](ftp://codisftp.codis.co.uk/Release/) 

Username: CodisFtpUser Password: C0di$FtpUs3r In practice we direct all customers to our website with direct links or www.codis.co.uk :\- 

### Copying to the Codis website

The final step of the release is when we request Raghu by email to copy these zipped folders to the Website. 

### Supported Platforms

The Supported Platforms page on the website needs to be updated. 

### Deployment

### The Standard Excelerator build process does the following

Deletes any old versions from the PrereleaseFolder   
Creates a zip file that includes the version number in its name in the PrereleaseFolder   
Copies that zip file to PreviousRelease   
Includes the manifest file in the zip   
Includes file versions in the manifest   
Includes a build reason in the manifest

  
Note: the Prerelease area only has the latest version of a file that includes the version number in its name. The PreviousRelease folder will have copies of all versions. 

## Prerelease version

### Prerelease version to a customer

A prerelease version can be made available on the Codis FTP Server, for a quick test onsite prior to general release. 

Copy the installation program zip file. (eg.NLJournalEx2\_2\.0\.0\.48\.zip)   
From: [\\\\Development\\PrereleaseFolder](file://///development/PrereleaseFolder) to   
Backend: [\\\\CodisFtp\\PreRelease](file://///codisftp/PreRelease) 

Ask the customer to download the renamed file from: Frontend: [ftp://codisftp.codis.co.uk/Prerelease](ftp://codisftp.codis.co.uk/Prerelease) 

Username: CodisFtpUser   
Password: C0di$FtpUs3r 

## Previous released versions

### Previous released versions are saved

Previous released versions are saved in case we have to test for a customer off site. We rarely do this as before we pass on support cases to development we test on the latest released version. (Except with the Enterprise version, as upgrading requires chargeable consultancy.) 

They are in the folder [\\\\CD01SR16104\\PreviousRelease](file://///cd01sr16104/PreviousRelease)

or for Enterprise Excelerator in the folder with the customer's name on, that is saved at the time of installation.
