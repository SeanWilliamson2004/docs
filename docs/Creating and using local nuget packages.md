---
title: Creating and using local nuget packages
tags:
- Development
- Nuget
description: Overview Nuget dependency management offers lots of benefits but can
  have a particular shortcoming. Sometimes a consuming project might depend on a…
created: '2019-12-24'
modified: '2023-09-11'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Creating%20and%20using%20local%20nuget%20packages.aspx
---

## Overview

Nuget dependency management offers lots of benefits but can have a particular shortcoming.  Sometimes a consuming project might depend on a package created by another project, but developers wants to work on both the consuming and the dependency source code, and debug both.  To do this the version of the dependency source code and the dependency referenced by the consuming project must be the same.

The technique is a simple one to understand:

- The source project generates a nuget package with each local build
- The consuming project references the location where the package is created and uses the version of that package.

However, there are complications with this simple idea.

These are to do with ensuring any dependencies that are consumed by the source project are included as dependencies in the package being generated, and that the correct version is used.  

If the source project has a dependency *Dependency A* of version Xthen the source projects output package should include this as a dependency

There is a particular problem if the source project references a project, but that project generates a package and it is in fact that package of the correct version that is the dependency.

Source Project A outputs package A and references project B.  Project B outputs package B Version X.  Solution C consumes both Package A and Package B.  If B changes locally, then A will pick up these changes on a rebuild.  If C wants to use the latest versions of A and B, it will have to consume the package output of B directly, as well as A, and use the correct version of both.

## Generating a local package during the build

For changes to a source project to be used immediately by a consuming project, the referenced package has to be generated automatically by each local build.

The method we use to generate packages has evolved.  The functionality available in a .net core project to specify package generation settings is available in a .net framework project, except the settings must be entered by editing the project file rather than through the UI.  It is not necessary to invoke nuget pack (and its issue of ensuring that the nuget.exe is available) as we did.  Instead, reference the NuGet.Build.Tasks.Pack package and set the properties it uses.  A nuspec file is not needed.   Note that in both methods we use an environment variable to determine whether to target a local folder or nuget feed.  

```
PropertyGroup>

    <PackageId>$(MSBuildProjectName)</PackageId>

    <Version>$(GitVersion_NuGetVersionV2)</Version>

    <Authors>Codis Limited</Authors>

    <Company>Codis Limited</Company>

    <PackageOutputPath>$(SolutionDir)\output-packages</PackageOutputPath>

    <PackageOutputPath Condition="'$(LOCAL_NUGET_PATH)' != ''">$(LOCAL_NUGET_PATH)</PackageOutputPath>

    <GeneratePackageOnBuild>true</GeneratePackageOnBuild>

  </PropertyGroup>


```

See NuGet Metadata below to see how we apply this in CodisDevelopment.  

The old method, in case you find it in code:  

```
 <PropertyGroup>

      <PackageOutputPath>..\output-packages</PackageOutputPath>

      <PackageOutputPath Condition="'$(LOCAL_NUGET_PATH)' != ''">$(LOCAL_NUGET_PATH)</PackageOutputPath>

    </PropertyGroup>

    <Exec Command="..\Codis.Core\tools\nuget pack $(ProjectFileName) -Symbols -Version $(GitVersion_NuGetVersionV2) -OutputDirectory $(PackageOutputPath) -Properties Configuration=$(ConfigurationName) -IncludeReferencedProjects />


```

Don't use the post\-build task.  This is a property that is evaluated early in the build process, which means that it cannot use properties that have their values set after the post\-build property is evaluated but before the post\-build target is executed.  

See [https://docs.microsoft.com/en\-us/nuget/create\-packages/creating\-a\-package](https://docs.microsoft.com/en-us/nuget/create-packages/creating-a-package).  

[https://docs.microsoft.com/en\-us/nuget/reference/nuspec](https://docs.microsoft.com/en-us/nuget/reference/nuspec).   

## Nuget Metadata

In the main CodisDevelopment repo, we use the Directory.Build.props to set metadata consistently based on assembly versions set by gitversion, and properties.    

This includes setting different semantic versions methods based on whether the build is on the devops server or not, to achieve consist versions in both build scenarios.  

## Consuming a local package

Add the local folder as a package source for your PC.  This will be added to any sources defined in a local nuget.config.

### Caching

This can be an issue.  If the version of the package does not change after a code change in the source package, you will have to delete any local copies of the package, if the solution uses local copes (like CodisDevelopment does due to its settings in its nuget.config file)

Otherwise, you might have to run the command 

nuget locals all \-clear
