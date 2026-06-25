---
title: Creating a NuGet package using the Visual Studio 2015 Packager
tags:
- Development
- Nuget
description: This describes how to create a NuGet package using the Visual Studio
  Packager. This packager provides a convenient way to bundle dependencies into a…
created: '2017-01-25'
modified: '2020-07-03'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Creating%20a%20NuGet%20package%20using%20the%20Visual%20Studio%202015%20Packager.aspx
---

**This describes how to create a NuGet package using the Visual Studio Packager. This packager provides a convenient way to bundle dependencies into a package.**

**Be aware that this might have be superceeded by [https://codislimited.sharepoint.com/sites/Wiki/Pages/Creating%20and%20using%20local%20nuget%20packages.aspx](Creating and using local nuget packages.md)**

1. Download and install the Visual Studio NuGet Packager from bitbucket.org. (This is not the same as the Visual Studio NuGet package manager.) View the instructions on the web page.
2. Create a new project using the new template which can be found under Visual C\# projects.
3. Ensure you have the latest version of NuGet.exe in the project folder.
4. Follow this instruction: [https://bitbucket.org/azzlack/nugetpackager/issues/8/build\-of\-nugetpackager\-project\-never\-ends](https://bitbucket.org/azzlack/nugetpackager/issues/8/build-of-nugetpackager-project-never-ends) (until somebody fixes the template).
5. Follow the instructions from [the web page](http://www.eyecatch.no/blog/create-nuget-packages-easily/) including placing the assemblies in the .\\lib folder.
6. Build the project.
