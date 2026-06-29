---
title: Orchestrator Installation
tags: []
description: 1. Enable Web Socket Protocol in Server Manager Go to Server Manager
  > Manage >Add or Remove Features Go to Web Server > Application Development 2.…
created: '2024-04-24'
modified: '2026-04-24'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Orchestrator%20Installation.aspx
---

1\.      Enable Web Socket Protocol in Server Manager

1. Go to Server Manager \> Manage \>Add or Remove Features  
![image001.png](images/PublishingImages_Pages_Orchestrator_Installation_image001.png)
2. Go to Web Server \> Application Development  
![image003.png](images/PublishingImages_Pages_Orchestrator_Installation_image003.png)

2\.      Install IIS URL Rewrite:  

1. [URL Rewrite : The Official Microsoft IIS Site](https://www.iis.net/downloads/microsoft/url-rewrite)

3\.      Download and install Windows Hosting Bundle from :

1. [Download .NET Core 2\.1 (Linux, macOS, and Windows) (microsoft.com)](https://dotnet.microsoft.com/en-us/download/dotnet/2.1)  
![image005.png](images/PublishingImages_Pages_Orchestrator_Installation_image005.png)

4\.      Install Codis Sage200 System Settings

1. Download from DevOps: Sage 200 Web Services pipeline
2. Create new data base 'CodisMaster'  
![image007.png](images/PublishingImages_Pages_Orchestrator_Installation_image007.png)
3. Run CodisMaster.sql after updating first line: USE \[CodisMaster]  

C:\\Program Files (x86\)\\Codis Excelerator\\CodisIP\\CodisSage200SystemSettings  

Note: This SQL script is old and doesn't include salt column. To update the salt column, download Codis IP Hash Utility from pipeline and run the exe.  

Alternative for this is to run CodisMaster script downloaded from Sage1000 IP:  

[https://dev.azure.com/codislimited/CodisDevelopment/\_git/CodisDevelopment?version\=GBmaster\&path\=/Sage1000/V3/IP/Codis.System/CodisMaster.sql](https://dev.azure.com/codislimited/CodisDevelopment/_git/CodisDevelopment?version=GBmaster&path=/Sage1000/V3/IP/Codis.System/CodisMaster.sql)
4. Run Sage200CodisSystem  

![image009.png](images/PublishingImages_Pages_Orchestrator_Installation_image009.png)  

Test the connection details and save.
5. Complete the licencing process.

5\.      Run the SQL scripts for Orchestrator, should be run in the following sequence:

1. IPWebsiteApplicationFeature.sql – Run

this query on CodisMaster Database
2. Orchestrator.sql – Creates new database for Orchestrator
3. Orchestrator\_DefaultData\_1\.sql
4. Orchestrator\_Update\_1\.sql
5. Orchestrator\_Update\_2\.sql
6. Orchestrator\_Update\_3\.sql
7. Orchestrator\_Update\_4\.sql
8. Orchestrator\_Update\_5\.sql
9. Orchestrator\_Update\_6\.sql
10. Orchestrator\_Update\_7\.sql
11. Orchestrator\_Update\_8\.sql (Use when updating Orchestrator from old version where Export table name was GeolSocExport)

Once Orchestrator Database is created, update CodisMaster database with below update

Create following entry in MasterPolicy table in CodisMaster database 

| **Key** | **Description** | **IsConfigurable** | **CategoryID** | **ValueType** |
| --- | --- | --- | --- | --- |
| OrchestratorConnectionString | OrchestratorConnectionString | 0 | SystemParameters | String |

Create following entry in PolicyValue table in CodisMaster database and provide your Orchestrator database connection string in 'Value' column.

| **Key** | **Value** | **Description** |
| --- | --- | --- |
| OrchestratorConnectionString | Data Source\=\[ServerName];Integrated Security\=False;User ID\=\[UserId];Password\=\[Password];Initial Catalog\=\[DatabaseName];Connect Timeout\=30;Encrypt\=False;TrustServerCertificate\=False;ApplicationIntent\=ReadWrite;MultiSubnetFailover\=False | OrchestratorConnectionString |

DatabaseName: Orchestrator

6\.      Create Orchestrator website:

a.      Download artifacts from Orchestrator pipeline

b.      Open IIS and create a new application pool named 'CodisOrchestrator'  

![image011.png](images/PublishingImages_Pages_Orchestrator_Installation_image011.png)  

c.      Go to Sites\>Default Web site \> Add application

Application Pool: CodisOrchestrator (created above)

Path: Location of the artifact downloaded

 ![image013.png](images/PublishingImages_Pages_Orchestrator_Installation_image013.png)  

 ![image015.png](images/PublishingImages_Pages_Orchestrator_Installation_image015.png)  

d.      Update following details in the web.config

1. Update SelfURL to "http://localhost/Orchestrator/"
2. Update ServiceUserName \& ServicePassword in ConfigData folder.
1. Note: This user account should have Sage client installed and access to Sage as well.

4. Delete config data for other plugins that are not used.
5. Update Orchestrator AppPool to enable Load User Profile
1. CodisOrchestrator AppPool\> Advanced Settings\> Load User Profile \> Set as 'True'

7\.      Make following changes in applicationhost.config (%WINDIR%\\System32\\inetsrv\\config\\applicationHost.config)

1. Take backup before making any changes.
2. Update:   
\<sites\>  
                    \<site name\="Default Web Site" id\="1"\>  
                        \<application path\="/Orchestrator" **serviceAutoStartEnabled\="true"**  
                                              **serviceAutoStartProvider\="ApplicationPreload"** /\>  
                    \</site\>  
\</sites\>
3. Just after closing the \`sites\` element and after \`webLimits\` tag:  

                \<serviceAutoStartProviders\>  
                    \<add name\="ApplicationPreload" type\="Codis.Orchestrator.Server.ApplicationPreload, Codis.Orchestrator.Server " /\>  
                \</serviceAutoStartProviders\>

8\.      Updates in IIS:  

1. Set application pool properties for Orchestrator application pool to:
1. .NET CLR version: .NET CLR Version v4\.0\.30319  

Normally, for a .NET Core app, you'd use No managed code, but if you do that, the application preload option won't work.
2. Managed pipeline mode: Integrated

3. Right\-click on the same application pool and select "Advanced Settings". Update the following values:
1. Set start mode to "Always Running".
2. Set Idle Time\-Out (minutes) to 0\.

5. Open Advanced Settings of the application:
1. Set Preload Enabled \= True:

7. Go to Configuration Editor in the application  
![image019.png](images/PublishingImages_Pages_Orchestrator_Installation_image019.png)
1. Update doAppInitAfterRestart: True
2. Click on '…' at end of Collecttion (Count \= 0\)  
![image021.png](images/PublishingImages_Pages_Orchestrator_Installation_image021.png)
3. Enter:  
 hostName: (Leave it blank)  

 initializationPage: /hangfire  
![image023.png](images/PublishingImages_Pages_Orchestrator_Installation_image023.png)

9\. Update web.config in OrchestratorWeb to point toward correct endpoint address  
For export cancellation, use helper service.  
![image027.png](images/PublishingImages_Pages_Orchestrator_Installation_image027.png)  

10\.      Install the CodisSage200Webservices on the server using the installer.

1. This will create an application 'CodisSage200Services' under DefaultWebSite and will also create an application pool for it.
2. Update the web.config to point to correct server.
3. Copy Sage assemblies from Sage app services bin folder to wcf bin folder using Codis.WCF.Sage200Utility.exe

11\.   For Mollies and Resident we use customisation in NL to avoid duplication:  
 Download the artifact from : [https://dev.azure.com/codislimited/CodisDevelopment/\_build?definitionId\=150](https://dev.azure.com/codislimited/CodisDevelopment/_build?definitionId=150)  

Create folder named 'NLJournalCustomisation' in C:\\Program Files (x86\)\\Codis Excelerator\\Codis Sage200 Services\\bin  

Copy the dll from the artifact to the folder.  

Add the below key to web.config of the wcf service  

\<add key\="NLJournalAvoidDuplicatePluginPath" value\="C:\\Program Files (x86\)\\Codis Excelerator\\Codis Sage200 Services\\bin\\NLJournalCustomisation\\" /\>  

Run the sql script from the artifact.  

Note: We need to setup Identity as any Admin account that has access to Sage  

![image025.png](images/PublishingImages_Pages_Orchestrator_Installation_image025.png)
