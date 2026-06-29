---
title: Online Licensing System
tags:
- Development
- Licensing
- Online
description: The online licensing system (aka online licensing ) is the name given
  to the licensing system which added the ability for Codis software to be…
created: '2017-01-28'
modified: '2020-01-15'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Online%20Licensing%20System.aspx
---

The **online licensing system** (aka *online licensing*) is the name given to the licensing system which added the ability for Codis software to be licensed over the internet. 

## Features

Online licensing is backwards compatible with the other methods of licensing: **telephone licensing** and **.net licensing**.

## Troubleshooting client's errors

See [Online Licensing Trouble.aspx](Online Licensing Troubleshooting.md)  

## Patching a customer on enterprise

In case we need to patch a customer on enterprise, they need to be given the online licensing version of enterprise licensing. See this video for instructions on how to licence while our licensing web services aren't running. This video is mainly for developers/support. 

This video has voice instructions

## How to use

The following pages describe how to use the online licensing system: 

1. [Standard Online Licensing](Standard Online Licensing.md)
2. [Enterprise Online Licensing](Enterprise Online Licensing.md)
3. Terminal \& Citrix Online Licensing

## Test companies

### Setting up

Developers (and sometimes support) will need to set up a new company in CRM for every separate test instance of a system where licences will need to be configured (for standard, enterprise and citrix test environments). Follow these rules when setting up a test company: 

1. Mark the company as inactive
2. Tick the box "For Testing" when creating the company. This a new field. The company search screen now has this field, so developers can search just for test companies and test companies are hidden in the default search for everyone else.
3. Follow the naming convention below

### Naming Convention for Test Companies:

**test\_\<user\-name\> \<hyper\-name\>**

Where user\-name is the name of the person who has the local hyper on their pc. If the hyper is central then the name can just be Central. So e.g: 

- test\_Asim CS200V2011
- test\_Kurren CD01DTXP026
- test\_Central CS200V2015

Remember to check the for testing checkbox and set the company status to Inactive. 

### Searching

When searching for a test company, you can select those companies that are just for testing in the search screen:

![](images/Licensing_Licensing_Wiki_Images_Online_Development_SearchTestingCompanies.png) 

## Test licences

The system is backwards compatible with other licence types, including telephone and .net (v3\) licensing. These instructions show how to obtain a test licence. 

### .Net (v3\) test licences

After setting up your test company, follow the instructions in this video. 

Your browser does not support html videos. 

You may wish to group multiple test machines in the same test company to make managing licences easier. If this is the case, repeat the procedure adding another pc to the same company and create/assign licences accordingly. 

## Support Information

The below video is the recording of the [support training](https://codislimited.sharepoint.com/sites/Wiki/Licensing/Licensing%20Wiki/Documents/Licensing%20support%20training.pptx) given by Kurren Nischal on 10th October 2016\. 

This video has voice instructions

![](images/Licensing_Licensing_Wiki_Images_Online_Development_OAuth_Flow.JPG) 

## Developer information

| Development start date | 01\.08\.2014 |
| --- | --- |
| Development end date | 2016 |
| Language | VB.Net |
| Framework | 4\.5 |
| Visual studio version | 2015 |

### Technologies

The following technologies were used: 

- [Entity Framework v6 model first](https://msdn.microsoft.com/en-us/data/jj206878.aspx) for the data access
- [Castle Windsor](https://github.com/castleproject/Windsor/blob/master/docs/README.md) for dependency injection in some places, otherwise we construct the dependency tree manually (see "Example: poor mans DI" [here](http://blog.ploeh.dk/2012/11/06/WhentouseaDIContainer/))
- [Microsoft Silverlight](https://msdn.microsoft.com/en-gb/library/cc838218%28v=vs.95%29.aspx) for the CRM portion
- [RIA services](http://openriaservices.codeplex.com/releases) for the CRM silverlight client to read/write data
- [Nancy](http://nancyfx.org/)for the server side of the web portal
- [Durandal](http://durandaljs.com/) for the front end of the web portal
- [Gulp](http://gulpjs.com/) to compile the Durandal files into a single javascript file (requires Node JS installed)
- [OAuth 2](https://developers.google.com/identity/protocols/OAuth2) for authentication. On the desktop (Excelerator and other Codis applications) we use a loopback to log in and register. See "Option 2: Loopback" [here](https://developers.google.com/identity/protocols/OAuth2InstalledApp).

### Architecture

![Architecture.png](images/Licensing_Architecture.png)  

- Sometimes we need to add a person to CRM (e.g. when recording a primary user of a PC, we add that person as a person in the CRM company). The ASP.Net silverlight back end cannot communicate with the CRM web service directly so we have an intermediate web service which calls the CRM service called CRMData that the silverlight back end can call.
- The AppService is a WCF web service used to licence codis applications. Applications register with the web service and obtain licences.
- A licence is an encrypted XML string. It usually contains the computer ID which the client then checks against which prevents copying a licence to other machines.
- Licence XMLs are signed by the server to prevent being edited

### 

### Repositories

1. **Codis.Licence.Server.Core**   
Contains all entity framework classes for data access along with common code to register PCs, generate and encrypt licences, etc.
2. **Codis.Licence.Server.CRM**   
The ASP.Net silverlight back end and silverlight client.
3. **Codis.Licence.Server.Service**The AppService
4. **Codis.Licence.Online.Types**  
Contains DTOs and interfaces that all licencensing projects depend on (including the client side of licensing)
5. **Codis.Licence.Client**  
Contains libraries that Excelerator and other codis applications use. This has functions such as interacting with the web service, registering computers and obtaining licences. There are UI libraries and there is also an API library that an application can reference if they are headless, such as the Excelerator Enterprise web service.  
One project in this solution is **Codis.Licence.ComputerIdWriter.**This is used to generate a telephone activation code, when upgrading a computer that was previously licenced by telephone activation.
