---
title: Codis Sage 200 Webservices Installation
tags: []
description: Notes on the installation of Codis Sage 200 Webservices There is a pipeline
  build Sage 200 Web Services that generates an Installshield installer…
created: '2021-09-02'
modified: '2024-02-08'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20Sage%20200%20Webservices%20Installation.aspx
---

Notes on the installation of Codis Sage 200 Webservices  


  


There is a pipeline build **Sage 200 Web Services** that generates an Installshield installer using the Codis Sage200 System Settings.ism Installshield definition.

The **Sage 200 Services Release** releases this software.  
  


The installshield installs or upgrades a single website that acts as a web service for all the available webservices.  However, these multiple webservices **cannot coexist** in the same website due to some elements of their state being shared and these have to be split up if more than one webservice is being used.  


Due to an old interop dependency all Codis Webservices must run with 32 bit enabled.  


  


Copy all Sage dlls from Sage server into web service bin folder?  


  


https://codislimited.sharepoint.com/sites/Wiki/Development/Development%20Wiki/Documents/Sage%20200%20Web%20Service%20\-%20Walk%20Through.pdf\#search\=200%20web%20service

  


The Codis webservice web.config holds details of the Sage 200 server web services.  
  


\# Introduction   
Codis Sage200 Web(WCF) services. These are web services which are used to interact with Sage200 for insert/update of entities. We normally use these services from Orchestrator.   
  
\#Deployment1\. Get the installer from the published artifacts https://dev.azure.com/codislimited/CodisDevelopment/\_build?definitionId\=1472\. Install the service on the server using above installer.3\. This will create an application 'CodisSage200Services' under DefaultWebSite and will also create an application pool for it. However, we have to use separate application for each wcf service.4\. Copy the folder 'CodisSage200Services' application points to and make n copies of it. n referes to the number of services we need to deploy.5\. Create separate application for each WCF service required and create it's own application pool. Make sure the application pool's identity is set to 'Custom User account' and use the windows account for which Sage is installed on the system. You can verify it by checking registry for that user and it should have Sage registry value.6\. Point the application to it's own folder copied in above step.7\. Modify the web.config file of each service for ServiceName appsetting, and update it to one of the values i.e. CUSTOMERSSERVICE, NLJOURNALSERVICE, ORDERPAYMENTALLOCATIONSERVICE, PLINVOICESERVICE,    PURCHASEORDERSERVICE, SALESINVOICESERVICE, SALESORDERSERVICE, SLRECEIPTALLOCATIONSERVICE, SOPINVOICESERVICE, STOCKSERVICE, SUPPLIERSSERVICE etc.8\. In Web.config of application, change following below appsettings and replace //SAGE200C2020R1 with sage installation path.    Most probably, it would be c drive so for e.g. \\\\SAGE200C2020R1\\Sage\\Logon\\credentials.xml will become C:\\Sage\\Logon\\credentials.xml for credentialsFile key        \<add key\="credentialsFile" value\="\\\\SAGE200C2020R1\\Sage\\Logon\\credentials.xml"/\>        \<add key\="Sage200SiteLogonPath" value\="\\\\SAGE200C2020R1\\Sage\\Logon"/\>        \<add key\="ServerRootPath" value\="\\\\SAGE200C2020R1\\Sage"/\>6\. In Web.config, change following appsettings and replace //SAGE200C2020R1 with ServerName        \<add key\="ServiceBaseAddress" value\="https://SAGE200C2020R1:10443/"/\>        \<add key\="DomainName" value\="SAGE200C2020R1"/\>  
\#Troubleshooting1\. Most common issue comes while running application is "Sage installation folder not found". This usually comes when User configured in application pool doesn't have Sage installed for them.2\. If application pool closes automatically, make sure the User which is configured in application pool's identity, exists and correct password is provided.
