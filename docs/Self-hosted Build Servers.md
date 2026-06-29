---
title: Self-hosted Build Servers
tags: []
description: Documentation describing the demands of the builds and how those are
  meant with different build servers. As of 11 March 2026. See below for details…
created: '2026-03-11'
modified: '2026-04-01'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Self-hosted%20Build%20Servers.aspx
---

Documentation describing the demands of the builds and how those are meant with different build servers.   

As of 11 March 2026\.  

See below for details of Sage200TestEnvironment.  

**Build Servers**  

| **Name** | **Capabilities** | **Plan of what to do** |
| --- | --- | --- |
| CD01SR16104 | visualstudioSage1000TestDatabasesInstallshield2018BuildWIX | Ondemand |
| CD01SR16105 | visualstudioInstallshield2018BuildSage1000TestDatabasesWIX | Decommissioned |
| CD01SR22106 | visualstudioSage200TestEnvironment | No change |
| CD01SR22108 | visualstudioInstallshield2018BuildWIX | Provisioned |
| CD01SR22109 | visualstudioWIXSage200TestEnvironmentSage1000TestDatabases | Provisioned |

| **Builds** | **Purpose** | **Demands** | **Provided by(As\-Is)** | **Provided By****(Proposed)** |
| --- | --- | --- | --- | --- |
| **DevOps Builds** |  |  |  |  |
| Sage 1000 Gateway Build CodisDevelopment Repo | S1000 3\.5 Excelerator Test \- just tests code builds | visualstudio | CD01SR16105CD01SR22106 | CD01SR22109CD01SR22106CD01SR22108 |
| Build S1000 Excelerator YML | S1000 3\.3 Excelerator Release | visualstudioWIX | CD01SR16105CD01SR22106 | CD01SR22109CD01SR22106CD01SR22108 |
| Build S1000 Excelerator YML CodisDevelopment repo | S1000 3\.5 Excelerator Release | visualstudio | CD01SR16105CD01SR22106 | CD01SR22109CD01SR22106CD01SR22108 |
| Sage 200 Web Services | S200 WCF Service and System Settings | Installshield2018Buildvisualstudio | CD01SR16104CD01SR16105 | CD01SR22108 |
| S200 Gateway Build | S200 Excelerator Gateway | Sage200TestEnvironmentvisualstudio | CD01SR22106 | CD01SR22106CD01SR22109 |
| S200 Build And Release | S200 3\.5 Excelerator and release | visualstudioWIX | CD01SR16105CD01SR22106 | CD01SR22109CD01SR22106CD01SR22108 |
| Codis S1000 Enterprise | Sage 1000 3\.3 Enterprise | Installshield2018BuildvisualstudioWIX | CD01SR16104CD01SR16105 | CD01SR22108 |
| Sage 1000 Gateway Build | S1000 3\.3 Excelerator Gateway.  This doesn't seem to be used as a gateway though. | SQL ServerSage1000TestDatabases | CD01SR16105CD01SR16104 | CD01SR22109 |
| Common Folder Gateway Build | Excelerator 3\.5 Common folder build | visualstudio | CD01SR16105CD01SR22106 | CD01SR22109CD01SR22106CD01SR22108 |
| Codis.Log.Viewer | Log viewer build | visualstudio |  |  |
| Orchestrator |  | None \- runs on hosted server |  |  |
| **DevOps Releases** |  |  |  |  |
| Sage 1000 Enterprise Release V3\.1 | Codis S1000 Enterprise Release | None |  |  |
| Sage 1000 Standard V3\.1 Release | Build S1000 Excelerator YML Release | None |  |  |
| Sage 200 Standard Excelerator Suite V3\.1 Release | Build Sage 200 Excelerator YML Release (superceeded by S200 Build And Release) |  |  |  |
| **VS Build Pro** |  |  |  |  |
| Various V1 Excelerator build scripts | Build the V1 Excelerator product | Licenced C1 ProductInstallshieldVisual BasicVisual Build Pro | 104 | CD01SR16104 mounted on demand on SW PC |

## Sage200TestEnvironment

The Sage200TestEnvironment requires the following:  

1. SQL Server installed.
2. A Sage 200 server and client installed.
3. The build service must run as a Sage user.
4. No longer requires Excel as of PR 3140\.
5. Up to date Sage200Demo and Sage200Test databases installed (Sage200TestingDatabases [Sage200TestingDatabases \- Repos](https://dev.azure.com/codislimited/CodisDevelopment/_git/Sage200TestingDatabases)).
6. sa password as per 1Password (also in pipeline) to restore Sage200Demo database.

106 did use the admin user for the build service but this is considered a security risk.  
The user DevopsBuildService is used on 106 and 109\.  This must have the following:  
- A member of S200Users
- Temporarily a admin to allow login over RDP, then removed at end of setup.
- Sage 200 Client installed as user
- Rights to Log On As Service (secpol.msc)
- Be a Sage user (Update users in Sage Admin)
- Set up access to the two databases above.
- Member of role (finance) that has access to all the features.
- SOP User Permissions set up with all allowed and "WAREHOUSE" as the default warehouse.
- 
-
