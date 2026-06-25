---
title: Setting up FSLogix on AVD to work with Azure Storage account
tags: []
description: This page describes setting up fslogix to use an azure file share. This
  video describes a lot of the setup.…
created: '2025-10-06'
modified: '2025-10-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Setting%20up%20FSLogix%20on%20AVD%20to%20work%20with%20Azure%20Storage%20account.aspx
---

This page describes setting up fslogix to use an azure file share.  
  
This video describes a lot of the setup.  
  
https://www.youtube.com/watch?v\=1msGQEZ\_SkU\&t\=317s  


but this one picks up on a vital piece of information missing from the first video.  On this video https://www.youtube.com/watch?v\=yJqTJh2Tgxo\&t\=705s, you have to ignore the first 11\.30 before you get the info that is relevant.  


  


- The storage account should be dedicated to this task, as the secret used applies to the whole storage account.
- You should restrict access to the storage account to the VM network (another reason to dedicate it).
- Each AVD host has to have fslogix installed.  This is configured in intune.
- Each host should have this script run as local admin:

  
$fileServer\="\<storage account name\>.file.core.windows.net"$user\="localhost\\\<storage account name\>"$profileShare\="\\\\$($fileServer)\\\<file share name\>"$secret\=\<secret\>  
  
New\-Item \-Path "HKLM:\\SOFTWARE" \-Name "FSLogix" \-ErrorAction IgnoreNew\-Item \-Path "HKLM:\\SOFTWARE\\FSLogix" \-Name "Profiles" \-ErrorAction IgnoreNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "Enabled" \-Value 1 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "VHDLocations" \-Value $profileShare \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "ConcurrentUserSessions" \-Value 1 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "DeleteLocalProfileWhenVHDShouldApply" \-Value 1 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "FlipFlopProfileDirectoryName" \-Value 1 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "IsDynamic" \-Value 1 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "KeepLocalDir" \-Value 0 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "ProfileType" \-Value 0 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "SizeInMBs" \-Value 40000 \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "VolumeType" \-Value "VHDX" \-forceNew\-ItemProperty \-Path "HKLM:\\SOFTWARE\\FSLogix\\Profiles" \-Name "AccessNetworkAsComputerObject" \-Value 1 \-force  
  
- The script below should be run in the system context for the AVD VM.  This can be done in the VM configuration in Azure.  Operations\-\>Run
  
$fileServer\="\<storage account name\>.file.core.windows.net"$user\="localhost\\\<storage account name\>"$profileShare\="\\\\$($fileServer)\\\<file share name\>"$secret\=\<secret\>  
New\-ItemProperty \-Path "HKLM:\\SYSTEM\\CurrentControlSet\\Control\\Lsa" \-Name "LsaCfgFlags" \-Value 0 \-forcecmdkey.exe /add:$fileServer /user:$user  /pass:$secret
