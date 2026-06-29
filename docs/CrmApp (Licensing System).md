---
title: CrmApp (Licensing System)
tags:
- CRM
- Licensing
- Online
description: CrmApp is the name of a visual studio project used by developers in online
  licensing . It is a silverlight application that is hosted in an ASP.net…
created: '2017-01-25'
modified: '2017-01-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/CrmApp%20(Licensing%20System).aspx
---

**CrmApp** is the name of a visual studio project used by developers in online licensing. It is a silverlight application that is hosted in an ASP.net website, located in the project CrmApp.Web. The website is navigated to when the "licences" tab is selected when viewing a company in CRM. 

## Structure

The silverlight app was built with the aim of adding a **module** (*licence type*) with as little code as possible. Most of the project is plumbing, code for the individual modules is found under the **modules** folder. ### Modules

Under the **modules** folder, there is a folder for each licence type. There is also a **shared** folder for shared code used by all modules.  ## Plumbing

Most components take the following form:  

| ```  1
  2
  3
  4
  5
  6
  7
  8
  9
 10
 11
 12
 13
 14
 15 ``` | ``` Class MyView
        Inherits UserControl

        Sub New(vm as IViewModel)
               DataContext = vm

 '======

 Interface IViewModel

 '======

 Class BaseViewModel
        Implements IViewModel
  ``` |
| --- | --- |

Each module then inherits the base viewmodel to add a component: 



| ``` 1
 2
 3
 4
 5
 6
 7
 8 ``` | ``` Class StandardViewModel
        Inherits BaseViewModel       
  
 Class EnterpriseViewModel
        Inherits BaseViewModel
  
 Class TCViewModel
        Inherits BaseViewModel
  ``` |
| --- | --- |

The correct viewmodel is injected into the view depending on what section the user clicked on. 

E.g. **LicenceSummaryVM** Inherits **SummaryVM(Of LicencesSelectedEvent, EnLicence)** in the **Enterprise** module to add the following section: 

![](images/Licensing_Licensing_Wiki_Images_Online_Development_SummaryVm.png) Summary section
