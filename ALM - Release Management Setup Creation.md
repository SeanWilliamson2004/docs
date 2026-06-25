---
title: ALM - Release Management Setup Creation
tags:
- Development
- Application Lifecycle Management
description: Deprecated content This page describes the mechanisms used to create
  Installshield setups from within Release Management. Its intended audience are…
created: '2017-01-23'
modified: '2020-04-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/ALM%20-%20Release%20Management%20Setup%20Creation.aspx
---

**Deprecated content**

**This page describes the mechanisms used to create Installshield setups from within Release Management. Its intended audience are developers and release managers.** 

**It is out\-of\-date and should not be used.**

The technique we will use for setup creation going forward is as follows: 

- Setup creation will take place in Release Management.

I'm not sure this is the right place. The setups themselves are artefacts that could be created by the build and tracked in drop folders. But their setup will slow the build process \-all of them will have to be created\- which would be a problem for Continuous Integration. Also, the Setups are not needed or tested until the Release stage.

This can then be initiated by the Release Manager. 

- Builds leave dlls etc in a drop folder e.g   
CD01SR2K8004\\TFS\\TFSSage1000Drop\\Build Sage 1000\\\\CD01SR2K8004\\TFS\\TFSSage200Drop\\Build Sage 200 For All Configurations\\\\
- Installshield definitions are moved to   
CD01SR2K8004\\tfs\\Codis.BuildComponents\\TFS Installer. This area is part of a repo that can have changes committed.
- Installshield output is moved to sub\-folders of   
CD01SR2K8004\\tfs\\BuiltSetups. This will keep this changing content out of the repo.
- Setups will now be kept in a folder named   
CD01SR2K8004\\TFS\\Releases. There will be folders for each product. Within each setup folder there will be a folder named after the TFS Release name, that holds the setup and the Installshield logs.
- The PreviousRelease folder will no longer be used. The status of each release is now managed in Release Management rather than by movements between folders.
- The Release process will create an XML file named ReleaseVersion.xml in the drop location. This file will hold the build and release number.
- Installshield will be initiated using a Powershell Target Machine step. This is run on the development server. Note: it may be possible to move this to the TFS server as we should have a licence for a Stand Alone installshield. The Powershell scripts invoke the Installshield build using the IsCmdBld
- Installer definitions are moved to   
CD01SR2K8004\\TFS\\Codis.BuildComponents\\TFS Installer. These definitions have been amended to use a single path variable to source Assemblies. This path is overridden by the Powershell script to use the build drop folder for the build associated with the release.

This does mean that if you view the definition in Installshield, you will not be seeing the same artefact files used by the Release process.

- The Powershell scripts return the Installshield build output to the Release Management logs and will fail the step if the Installshield build fails. (Note: this was difficult \- Write\-Output output is lost if an error is thrown. Write\-Verbose was found to work).
- The Powershell script will also label the Installshield product version as the Release number.
- Follow the creation of the setup, the setup and its logs are copied from the default Installshield output folder to the   
Cd01sr2k8004\\tfs\\Releases in the folder described above.
