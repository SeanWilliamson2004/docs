---
title: ALM - Excelerator Release to Customers Deployment
tags:
- Application Lifecycle Management
- Release
description: 'The following areas have to be deployed to: FTP Site All released files
  are stored on the ftp Each Excelerator Product Range have their own folders…'
created: '2017-01-16'
modified: '2018-08-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/ALM%20-%20Excelerator%20Release%20to%20Customers%20Deployment.aspx
---

The following areas have to be deployed to:

## FTP Site

All released files are stored on the ftp Each Excelerator Product Range have their own folders For Example.  See [Codis FTP and SFTP.aspx](Codis FTP and SFTP.md) for more details on accessing the FTP area.

| Link | Description |
| --- | --- |
| [Sage 200 Standard Excelerators](file://///codisftp/Release/Sage_200_Standard_V3) | Sage 200 Standard Excelerators |
| [Sage 1000 Standard Excelerators](file://///codisftp/Release/Sage_1000_Standard_V3) | Sage 1000 Standard Excelerators |
| [Sage 1000 Enterprise Excelerators](file://///codisftp/Release/Sage_1000_Ent_V3) | Sage 1000 Enterprise Excelerators |

## Updating the Release

The files are prepared for release. Each file is zipped and **the version number must be removed from the Zip file name** and the files are then copied into the Product Range release older (see table above).   
**NOTE:** For Sage 200 there are subfolders for the different Sage versions.The files on the FTP site are all zipped folders with names that do not include the version numbers. The setup file in the zip does include the version number, so you can view the contents of these folders to confirm the versions if required. The following screen shot shows both the unzipped files and the renamed zipped folders.

![](images/Support_Support_Wiki_Images_Release.png) 

The files highlighted in the screenshot above, were in pre\-release at the start of the test cycle but were not ready to be tested so they will be removed from this test folder and not copied to the release folder. The network address of the release folder is:\-   
192\.168\.3\.212\\Release\\Sage\_1000\_Std\_V3 The following is the front end address for information only. [ftp://codisftp.codis.co.uk/Release/](ftp://codisftp.codis.co.uk/Release/) Username: CodisFtpUser Password: C0di$FtpUs3r In practice we direct all customers to our website with direct links or www.codis.co.uk :\-

## Copying to the Codis website

The final step of the release is when we request Raghu by email to copy these zipped folders to the Website.

## Supported Platforms

The Supported Platforms page on the website needs to be updated.

## Releasing Enterprise versions

The release of the Enterprise version is similar except that they are not copied to the website. Codis staff install these for clients and we save a copy of the version we install with the customer name in the folder. The install files for Enterprise are in the folder   
CD01SR2K8004\\PrereleaseFolder\\Enterprise Setups\\V3 Two files also required SystemSettings and IPwebsiteSetup are in the folder   
CD01SR2K8004\\PrereleaseFolder\\Enterprise Setups Copy all of these files to the testing folder, and after testing to the release folder

## Release Hyper for Sales

A new hyper is prepared for Sales with the latest releases of the software.

## Prerelease version

### Prerelease version to a customer

A prerelease version can be made available on the Codis FTP Server, for a quick test onsite prior to general release.

Copy the installation program zip file. (eg.NLJournalEx2\_2\.0\.0\.48\.zip)   
From: \\Development\\PrereleaseFolder to   
Backend: \\CodisFtp\\PreRelease

Ask the customer to download the renamed file from: Frontend: [ftp://codisftp.codis.co.uk/Prerelease](ftp://codisftp.codis.co.uk/Prerelease)

Username: CodisFtpUser   
Password: C0di$FtpUs3r

## Previous released versions

### Previous released versions are saved

Previous released versions are saved in case we have to test for a customer off site. We rarely do this as before we pass on support cases to development we test on the latest released version. (Except with the Enterprise version, as upgrading requires chargeable consultancy.)

They are in the folder \\CD01SR2K8004\\PreviousRelease   
or for Enterprise Excelerator in the folder with the customer's name on, that is saved at the time of installation.
