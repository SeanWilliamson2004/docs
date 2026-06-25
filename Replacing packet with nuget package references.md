---
title: Replacing packet with nuget package references
tags: []
description: See paket vs nuget vs nuget package references.aspx for a discussion
  as to why this has to be done. paket provides a few advantages over package…
created: '2019-12-23'
modified: '2020-09-08'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Replacing%20paket%20with%20nuget%20package%20references.aspx
---

See [paket vs nuget vs nuget package references.aspx](paket vs nuget vs nuget package references.md) for a discussion as to why this has to be done.

paket provides a few advantages over package references.  Package references only provides the package manager for managing the application of consistent dependency versioning across a solution with numerous projects.  The techniques below described below are an alternative means of applying consistent versioning.

The idea is:

- Use the directory.build.props and directory.build.targets functionality to ensure that each project loads central property setting and target setting files placed at the root of the solution.
- Apply package references in the central target file, but references use versions held in the central property file. Package references are applied conditionally based on build properties.
- Set the build properties that choose whether to apply references local to a folder structure, meaning that package references can be applied to single projects or sets to projects based on the folder structure.  Ideally set these properties externally to the directory.build.props to avoid this files where possible.

This has been applied in the CodisDevelopment and Codis.Licence.Client repos.  

- Version numbers are defined in a file Directory.Build.Versions.props.
- References are added in the Directory.Build.targets file.
- Which reference is applied to a project is determined by IncludeReferences.props files in the project folder or higher folders in the hierarchy.  Sometimes it is defined in the Directory.Build.props.

The targets file also adds a target that lists the versions that have been defined for references that are applied to the project being built.
