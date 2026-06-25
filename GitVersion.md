---
title: GitVersion
tags: []
description: Gitversion is an open source tool that can help you acheive semantic
  versioning in your project based on the status of the Git repository.…
created: '2019-12-27'
modified: '2019-12-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/GitVersion.aspx
---

Gitversion is an open source tool that can help you acheive semantic versioning in your project based on the status of the Git repository.

Documentation can be found at: <https://gitversion.net/docs/>

Codis is using GitVersion as its standard versioning tool.  It provides a few versioning models that can be used to fit with our working practices and (once you know what to do) integrates nicely with WIX to version setup msi and exes.

## Non\-WIX Projects

For a non\-WIX project, all you have to do to use it is:

1. Add a package reference to the project.
2. Apply your GitVersion versioning model to fit with your branching strategy.
3. Remove all Assembly\*Version properties from AssemblyInfo.vb etc.
4. Add a GITVersion step to your build to version the AzureDevOps pipeline.

### 

### Add a package reference to GitVersionTask to the project

For the projects in the CodisDevelopment, we force this for every project using the Directory.Build.targets at the core of the repo.

### Apply your GitVersion versioning model to fit with your branching strategy.

For our CodisDevelopment repo, we use a MainLine branching strategy. GitVersion can be configured recognises this and can be told to only increment when a merge into master takes place. This in turn means that each increment demands a change. (It does also mean that a repeated build will get the same build number which isn't so good but maybe not a big problem). We can specify the nature of a change in the PR title, which because the commit description. I think this is the right place to be specifying this. The resulting version number is 3 segments so can be used for the installer.  
GitVersion can be used from the msbuild as well. If this can be fired only when not building in DevOps (as it will fired a different way in there) then it may be possible for it to generate the same version number that devops would use, keeping to two in sync.

You versioning model is specified in the gitversion.yml file.  You will need to add one if there isn't one there already.  It can contain just:  
mode: Mainline  
branches: {}  
merge\-message\-formats: {}

### Remove all Assembly\*Version properties from AssemblyInfo.vb etc.

Gitversion will generate and apply a version number to all assemblies.  This will increment the assembly version.  In the past we have avoided this because we were finding inconsistencies that were breaking our local builds.  However, this problem is removed by using a tool that dynamically applies a consistent version number to all assemblies being built.  Also, having separate target for builds for the different products stops clashes that used to occur when a different version was being used for each project, but the outputs were copied to the same folder.

### Add a GITVersion step to your build to version the AzureDevOps pipeline.

There is a Gitversion pipeline task.  It will version the build using the same alogorithm as the assemblies and exes.  

### Tag the Repo with your starting version number

You can do this for the master branch using the Tags tab in DevOps.  Add a tag e.g. 1\.0\.0 to give a starting version number of 1\.0\.0\.  You may then need to merge the master branch into your working branch.

  
 

## WIX Projects

Gitversion can be used to apply the same versioning methodology as that being used to version assemblies.  This avoids any challenges involved in retrieving versions from target assemblies.

However, the application is more difficult.   The best way to apply GitVersion is to find a project that already works and copy the relevant lines from the wixproj file, adjusting paths as appropriate.  

You need to:

1. Import the properties at the beginning.
2. Import the targets at the end.

## Versioning nuget packages

Gitversion can be used to version nuget packages generated during a build.  This can be extremely useful when multiple projects are in a solution that products multiple packages.  You can ensure that the same version number is being used by using GitVersion.  The number will be consistent because it depends on the Git repo.  See https://codislimited.sharepoint.com/sites/Wiki/Pages/Creating%20and%20using%20local%20nuget%20packages.aspx
