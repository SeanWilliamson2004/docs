---
title: Sage 200 Extra Online - How to modify SQL data in Sage 200 Extra Online
tags:
- Support
- Sage
- Sage 200
- Sage 200 Extra Online
- SQL
description: Sage 200 Extra Online - How to modify SQL data in Sage 200 Extra Online
  Article number 33849 Products Sage 200 Extra Sage 200 Extra Online Last…
created: '2017-02-23'
modified: '2018-07-19'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Extra%20Online%20-%20How%20to%20modify%20SQL%20data%20in%20Sage%20200%20Extra%20Online.aspx
---

# Sage 200 Extra Online \- How to modify SQL data in Sage 200 Extra Online



| | | Article number | | --- | | 33849 | | | --- | --- | --- | | | Products | | --- | | Sage 200 Extra     Sage 200 Extra Online | | | | Last updated | | --- | | 05/07/2016 10\.05 AM | | | | Article type | | --- | | Information | | | | TFS number | | --- | | *Not specified* | | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |



| | Summary | | --- | | At times it may be necessary to modify data on SQL Azure to correct issues, for example following a network disconnection during processing.As the SQL Azure data is not readily available to modify directly, the issue must be addressed via a SQL script uploaded as an add\-on.**Note:** This article is provided to assist you with making modifications to data where you have already consulted with Sage 200 Support. As per the terms and conditions in the Software Licence Agreement (SLA), modifications to the database are not supported unless otherwise advised by the Support team. | | Answer | | **Note:** If your database performance is listed as S1 in SEOS, you must use SQL Management Studio 2016 to restore the data as it will not restore to versions 2012 or 2014 of SQL Management Studio.Download a bacpac to view the SQL data:Within SEOS (Sage ERP Online Services) you must download a backup of the data to restore locally. This may be a nightly automatic backup or an on\-demand backup of the company and information on how to do this can be found [here](http://www.sage.co.uk/asksage/viewarticle.asp?p_faqid=31780).Import the bacpac into SQL Server Management StudioWithin SQL Server 2012 SP2, right click 'Databases' and select 'Import Data\-tier Application…' and follow the wizard to import the data.You can now directly interrogate the data in SQL or open the data in Sage 200 by connecting the database in SA in the usual way.Write a script to correct the issueCreate your query and save the script.Ensure the site is backed\-up and re\-test your script locally (important).Backup the database – this may take some time depending on the size of the database.Your script should be re\-tested, preferably on a freshly restored copy of the data to ensure it has the desired results.Package the script to create an SDBX fileDownload the Sage 200 Add\-on Packager from [here](https://my.sage.co.uk/downloads/detail.aspx?did=faa4ae2c-5800-41d0-a93a-4f251d6cb303) \> New \> Add file \> Save.Upload the Add\-on via SAEnsure all users are logged out of Sage 200 Extra Online.Within SA \> Add\-on's \> Add the SDBX file.**Note**: When asked if you want to run the script for all companies, choose 'No' and update only the company required. Remove the SDBX from Add\-on's when complete.Note: Also refer to [this page](Steps to restore bacpac to SQL.md) for information about restoring BACPAC to SQL. | |
| --- | --- | --- | --- | --- |
