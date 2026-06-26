---
title: LicensingCommon
tags:
- Development
- Online
- Licensing
description: LicensingCommon is the name of a visual studio project used by developers
  in online licensing . It is a common library which is referenced by most of…
created: '2017-01-28'
modified: '2017-01-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/LicensingCommon.aspx
---

**LicensingCommon** is the name of a visual studio project used by developers in [online licensing](Online Licensing System.md). It is a common library which is referenced by most of the other **server** projects in the solution. 

Do not reference this project from any projects that will be installed on the users machines.

## Common

The following folders are under the **Common** folder: 



| **Folder** | **Description** |
| --- | --- |
| OAuth | Used to obtain a person (and subsequently their company) from CRM, given their email address. They must be a **licence administrator**, otherwise an exception will be thrown. |
| Standard | Contains server side tasks to do with standard licensing. E.g. Registering a PC or checking in. |
| TerminalCitrix | Same as standard, but for Terminal/Citrix licensing |
| Enterprise | See above |
| Xml | Contains classes used to decrypt and encrypt objects into sealed and signed XML activation strings |

## Accessing CRM

Classes under the CrmAccess folder are used for this. 

## Data access

The database is accessed using [Entity Framework model first](https://msdn.microsoft.com/en-us/data/jj206878.aspx), version 6\. 

### Diagrams

The model is split into 3 diagrams, one for each licence type. 

### Contexts

Usually only one licence type will need to be accessed at a time. Because of this, the [repository pattern](https://msdn.microsoft.com/en-us/library/ff649690.aspx) is used to split the single context containing all licence types into one for each licence type. A similar approach is taken in [CrmApp (Licensing System)](CrmApp (Licensing System).md). 

### Eager loading

To save time, entities must be [eager loaded](https://msdn.microsoft.com/en-us/data/jj574232.aspx) into the context before being used. This is usually done with a string.



| ``` 1 2 3 ``` | ``` ' Load all blogs, all related posts, and all related comments   ' using a string to specify the relationships  Dim blogs2 = context.Blogs.Include("Posts.Comments").ToList()  ``` |
| --- | --- |

### XML Transforms

Tables in the CRM database do not have any primary keys. Because of this, entity framework does not allow insertion into these tables (tables added for the licensing system do have a primary key, so this only applies to existing CRM tables such as Company and Person). There is a [fix](http://stackoverflow.com/a/21768789/1282944) that can be applied to the XML of the EF Schema to allow insertion into these tables. The file **Transform.xslt** is an XML transform that applies this fix. This transform is run on build, which can be seen by opening up the project file in a text editor and looking for the following: 



| ``` 1 2 3 4 5 ``` | ``` <Target Name="BeforeBuild">   <XslTransformation XmlInputPaths="DataAccess/Model/LicenceModel.edmx" OutputPaths="edmxTransformedTemp.edmx" XslInputPath="DataAccess/Model/XmlTransforms/Transform.xslt" />   <Copy SourceFiles="edmxTransformedTemp.edmx" DestinationFiles="DataAccess/Model/LicenceModel.edmx" />   <Delete Files="edmxTransformedTemp.edmx" /> </Target>  ``` |
| --- | --- |
