---
title: Comparing versions of Excelerator
tags: []
description: When Excelerator is installed, it registers the Addin, and this registration
  points to assemblies in a specific folder. You can locate this folder in…
created: '2023-12-05'
modified: '2023-12-07'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Comparing%20functionality%20in%20different%20versions%20of%20Excelerator.aspx
---

When Excelerator is installed, it registers the Addin, and this registration points to assemblies in a specific folder. You can locate this folder in Excel by going to File, then Options, and finally Add\-ins. The registration process does not take into account the version of Excelerator, so it won't matter if a different version is present in that location. Therefore, to run a different version, you can follow these steps:  

1\. Suppose you have installed Version 2\.

2\. Get a copy of Version 1 assemblies and copy them to another folder. For example, if the installation folder is %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard Excelerator, you could use %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard ExceleratorV1\.

3\. To use the old version, rename %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard Excelerator to %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard ExceleratorV2, and rename %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard ExceleratorV1 to %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard Excelerator.

4\. To use the new version, rename %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard Excelerator to %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard ExceleratorV1 and %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard ExceleratorV2 to %localappdata%\\Codis Limited\\Codis Sage 200 SPE2019 Standard Excelerator.

You can also automate these steps using a script.
