---
title: Using Sage 200 Assembly Packages
tags:
- Development
- Sage 200
description: In our Sage 200 Excelerator products we use Sage's own API to apply many
  of the business rules and to perform CRUD operations. We attempt to support…
created: '2020-10-19'
modified: '2020-10-19'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Using%20Sage%20200%20Assembly%20Packages.aspx
---

In our Sage 200 Excelerator products we use Sage's own API to apply many of the business rules and to perform CRUD operations.  

We attempt to support multiple major Sage 200 releases, as well as differing minor releases within each major release.  Doing this does present a number of challenges.  The assemblies that you use have to be compatible with the server version of Sage you are connecting to.  They also have to be compatible with one another.   

Note: for the last 2 years Sage have operated a rolling release for Sage 200\.  New releases are made every quarter or so.  

New versions of assemblies were released with new major and minor releases.  Sometimes the interface changes \- new properties or methods are added, and even breaking changes have occurred. We have created some packages to allow development of solutions for each of these major releases.

**Important:**

- **There is not a package for every version of Sage.  There is a package for every version of the interface.**
- **The package does not contain all the Sage assemblies.  It contains only the assemblies we directly reference.**
- **We do not deploy these assemblies**

In a production environment (i.e a customer's PC), this works by using our [Sage 200 Excelerator Assembly Resolution.aspx](Sage 200 Excelerator Assembly Resolution.md "Sage 200 Assembly Resolution alogrithm").  This will attempt find the assemblies installed on the PC and run using those.  It means that far fewer versions of the assemblies need to be packaged, although it can sometimes fail when e.g. old registry key values are in place.  

In a development environment different solution and project configurations are used for each version of the code that is needed for different Sage interfaces.  Again \- this is not the same as having a configuration for each Sage version, major or minor (or rolling release).  A version of code is needed for each change of the interface where a new property or method is introduced (or removed), and for each change of Sage assembly version. (These two criteria coincide).   We have used the techniques described here [Replacing paket with nuget package references.aspx](Replacing packet with nuget package references.md) to centralise the definition of these versions, meaning that you only need to define :

    \<UsesSageAPIObjects\>true\</UsesSageAPIObjects\>  
and use the correct project/solution configuration to reference the correct package.  The names of the packages used can be found in the central Directory.Build.targets file.

The solution or project is also used to specify compile constants to allow code to be precompiled in or out.

However, on a development machine it is still possible that the version of  the assemblies in the packages do not exactly match the version of Sage being run and also, so we must used the same assembly resolver used in a production environment, which is loaded by default by the S200 Excelerator framework.

So, **you will reference the package assemblies but load the installed assemblies.**

As the Assembly resolver only resolves assemblies that aren't resolved by the default mechanisms, it is important not to resolve the package assemblies, but to only resolve the assemblies installed on the PC.  As such:  

**You must not have package assemblies in the runtime folder.**  

To do this all test harnesses, unit tests and Excelerators must remove the Sage assemblies in an after build event.  The Excelerator addin does this, so all Excelerator modules including new ones should run OK.  But it is an easy mistake to make when creating new test projects.

 cd $(TargetDir)

 del Sage\*.dll
