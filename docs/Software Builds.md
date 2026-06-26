---
title: Software Builds
tags:
- Development
- Build
description: A Software Build is the process of producing an installer that a customer
  can download, after the code for the software has been developed. This page…
created: '2017-01-25'
modified: '2017-10-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Software%20Builds.aspx
---

A **Software Build** is the process of producing an installer that a customer can download, after the code for the software has been developed. This page describes the software and configuration files used for builds of Codis software. It is aimed at developers. 

## Overview

Builds are not the same as software releases. Builds can be made very frequently \- to ensure the software compiles and to run automated tests. A releases happens when the product of the build \- the installer or installers are copied into a testing or release area. 

## V3 Builds

V3 builds now form part of the [Application Lifecycle Management at Codis](Application Lifecycle Management at Codis.md) and take place in TFS.

## V1 Builds

Codis uses [Visual Build Pro](http://www.kinook.com/VisBuildPro/) build scripts to build its software. The scripts are kept on the development server in c:\\development\\BuildScripts. A script can run other scripts, allowing builds to be nested. 

In V1, there are multiple installers create \- one for each module. There are multiple build scripts including ones for COM libraries that are reused in other builds. There aren't any scripts that initiate multiple builds. 

In V1, there are single installers for each of the products, except for the server side components of the Enterprise products. The aim has been to have a few controlling build scripts that will build all the assemblies required for a product, not just a module in a product. This will ensure that all assemblies are compatible.
