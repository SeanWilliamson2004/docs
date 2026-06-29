---
title: ALM - Build Retention and Drop Folder Maintenance
tags:
- Development
- IT
description: Builds are run frequently. Any pull request or push to a branch with
  a pull request, and any completed pull requests results in a build (see Software…
created: '2017-10-10'
modified: '2017-10-11'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/ALM%20-%20Build%20Retention%20and%20Drop%20Folder%20Maintenance.aspx
---

Builds are run frequently.  Any pull request or push to a branch with a pull request, and any completed pull requests results in a build (see [Software Release Procedures).](ALM - Software Release Procedures.md)  Only some builds are released.

The build processes produce output that is placed in drop folders for use by Release Management.  Builds that are released are marked as retained by the Release Management.   After a period of time, it is unlikely that the record of the build and it's drop folder is required and policies and processes can be applied to have this record cleaned.   The frequency of the builds can result in disk space being consumed by the drop folder output.  TFS applies Retention Polices to builds that will clean up build records after a period of time.  Although it is not clear whether these work, regardless the clean up will not remove the drop folder output as this lies outside any defintion of the build to TFS.  

If the retention policy does not work, then it is fairly straightforward to select multiple builds in TFS and then click on the elipse on one of them and select "Delete.

To clean up the drop folders use [\\\\Cd01sr16104\\tfs\\Codis.BuildComponents\\PowershellScripts\\BuildCleanUp.ps1](file://///cd01sr16104/tfs/Codis.BuildComponents/PowershellScripts/BuildCleanUp.ps1) run from the powershell.  The script should be amended to set the file prefix and drop folder variables.

```
$filePrefix="1016*"

$dropFolderRoot="\\Cd01sr16104\tfs\TFSSage1000Drop\" 



$filePrefix="17\.*"

$dropFolderRoot="\\Cd01sr16104\tfs\TFSSage200Drop\" 


```

The filePrefix is the start of the name of the build folder.  The dropfolder is where the script should look for folders.  It will look in sub\-folders of the folder below given dropFolder.

The script reads a list of builds from the TFS Server.  It then look at each sub\-folder whose name matches the prefix and check if it is on the list.  If it isn't, it will delete the folder.  The name of folders deleted and kept are written to the console.
