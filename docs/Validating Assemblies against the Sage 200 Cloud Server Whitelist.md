---
title: Validating Assemblies against the Sage 200 Cloud Server Whitelist
tags:
- Development
- Sage 200
description: This page describes how to validate assemblies against the Sage 200 Cloud
  Server whitelist rules. It is aimed at developers only. Overview Sage 200…
created: '2017-01-26'
modified: '2022-01-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Validating%20Assemblies%20against%20the%20Sage%20200%20Cloud%20Server%20Whitelist.aspx
---

**This page describes how to validate assemblies against the Sage 200 Cloud Server whitelist rules. It is aimed at developers only.**

## Overview

Sage 200 Extra Cloud allows 3rd assemblies to be deployed to the Cloud server. However, there are stringent security rules in place and many commonly used coding techniques and references are not allowed. For instance, any use of System.Reflection is not allowed. You cannot call GC.Collect 

Assemblies are deployed to the cloud server via Sage Add\-on packages. The Add\-On Packager allows files to validated as allowed on the cloud server. If valid, the Add\-on package can then be installed on the server. Assemblies are validated against a white list of allowed assemblies. This white list is required for the validation and it is available at   
development\\development\\whitelist.xml. 

## Validating using the Add\-on Packager

The Add\-on Packager can be run in any Sage 200 environment. You may choose to run it on a Sage 200 On\-Premise Hyper\-V. The video below describes how to validate assemblies. 

The video does not mention that you should copy assemblies that you want to validate on to Hyper where you are running the validation. If you then make code changes and want to validate again, then copy over the new assembly into the same location, and run the validation again.
