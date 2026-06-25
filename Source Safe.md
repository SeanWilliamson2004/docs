---
title: Source Safe
tags:
- Development
- Source Safe
description: Microsoft Source Safe is a system used by developers to manage projects
  which require multiple developers to work on the same codebase. Adding…
created: '2017-01-27'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Source%20Safe.aspx
---

[Microsoft Source Safe](https://msdn.microsoft.com/library/ms181038%28en-us%2cvs.80%29.aspx) is a system used by developers to manage projects which require multiple developers to work on the same codebase. 

## Adding projects

 To add a project to source safe, assuming your projects are contained in a single solution and reference each other by project references rather than dll references: 

1. Remove the project from the solution (right click \- remove)
2. Move the folder that contains the project into the path C:\\Development\\VB.NET
3. Open the project. This should create a new visual studio solution containing only the project
4. Go to the project properties (right click \- properties) and change the **build output path** to C:\\Development\\VB.NET\\Assemblies
5. Compile the project
6. Right click the project, select **source control** then **add solution to source control**
7. If a save dialog appears, click save (with the default path)
8. Log into source safe if prompted
9. Remove the **.root** suffix after the project name, leave all other paths the same
10. Click add
