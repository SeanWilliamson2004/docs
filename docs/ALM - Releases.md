---
title: ALM - Releases
tags:
- Development
- Application Lifecycle Management
description: Release now output to Sharepoint locations rather than file systems.
  The sharepoint site is AllItems.aspx . Release pipelines output to Pre-Test.…
created: '2017-10-20'
modified: '2019-09-13'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/ALM%20-%20Release%20Definitions.aspx
---

Release now output to Sharepoint locations rather than file systems.  

The sharepoint site is [AllItems.aspx](/sites/builds/Shared%20Documents/Forms/AllItems.aspx?sortField=Modified&isAscending=false&viewid=00000000-0000-0000-0000-000000000000).  Release pipelines output to Pre\-Test.  Release stage can optionally copy to either Beta (for beta test releases) or Release (for full release).  Pre\-Test keep a full history of releases and the file names include the release name.  (Deleted or abandoned release output is cleared down.)   Beta and Release folder contain only the latest release.

The following releases are active:  

| **Release Name** | **Purpose** | [Build](ALM - Active Builds.md) | **Outputs (Test)** |
| --- | --- | --- | --- |
| Sage
 1000 Standard V3\.1 Release | Main release for Sage 1000 Standard Excelerator.  No versions prior to V3\.1 are supported now. | Build S1000 Excelerator YML |  |
| Sage
 200 Standard Excelerator Suite V3\.1 Release | Main release for Sage 200 Standard Excelerator. | Build Sage 200 Excelerator YML | S200Standard\\StandardSage200v\<sage version\>ExcelerateSuite for sage versions 2011, 2013, 2015, 2016, WE2018 |
| Sage
 1000 Enterprise Release V3\.1 | Main release for Sage 1000 Enterprise Excelerator.  No versions prior to V3\.1 are supported now. | Build Sage 1000 V3\.1 | Enterprise client: EnterpriseExceleratorNET V3\.1\\\<release name\>\\EnterpriseClientSuite.exeEnterprise services: EnterpriseExceleratorNET V3\.1\\\<release name\>\\\<various\>.exe**Note that this has the same output folder as "Sage 1000 Enterprise Release V3\.1 \- Codis IP".  It also copies from the same source at the end.  This means that the result of the last release of "Sage 1000 Enterprise Release V3\.1 \- Codis IP" will be included in the output.** |
| Sage 1000 Enterprise Release V3\.1 \- Codis IP | Main release for Codis IP Website and and system settings program | Build Sage 1000 V3\.1 | IP System settings Enterprise services: EnterpriseExceleratorNET V3\.1\\\<release name\>\\SystemSettings.exeEnterpriseExceleratorNET V3\.1\\\<release name\>\\IntegrationPlatformSetup.exe |
| Sage
 200 DutyPoint Excelerators Release V3\.1 | A temporary release needed for Duty Point. | Build Sage 200 For DutyPoint All Configurations | StandardSage200ExceleratorSuiteV3\.1\\DutyPoint Setups\\\<sage version\>\\StandardSage200v2016ExceleratorSuite\_\<release name\>.exe |
| Revital
 Import Release | Releases the Revital Import product | Build Revital Import | \\RevitalImport\\\<release name\>\\setup.exe |
| Geological
 Society Plugins Release | Releases GeoSoc society Care\-S200 interface product. | Build Geo Soc Plugins | Zipped addin files.  \\GeoSocPlugins\\\<release name\>\\\<module\>. |
