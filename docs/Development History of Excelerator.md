---
title: Development History of Excelerator
tags:
- Development
- Training
description: Overview Codis has been developing software for approximately 20 years.
  This has led to a broad range of software solutions with different…
created: '2019-09-12'
modified: '2019-09-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Development%20History%20of%20Excelerator.aspx
---

# Overview

Codis has been developing software for approximately 20 years.  This has led to a broad range of software solutions with different architectures that may sometimes seem difficult to understand.  By understanding the history of the software development in the company, these can make more sense.

# Codis' Relationship with Sage

Codis was founded by former Sage Tetra employees.  Tetra was a company that was bought by Sage.  It developed a UNIX based ERP system that was ported to Windows Server.  This product became known as Sage 500 and Sage 1000\.  (Sage 500 has been discontinued).  Sage 1000 tended to sell to middle tier companies and was often kept as they grew into upper middle tier companies.  Some significant household names in the UK used or uses Sage 1000\. Sage 200 was another company purchased by Sage.  It was a .net solution running on windows servers and PCs and sold more to the lower\-middle tier. 

Codis has provided consultancy around and software that integrates with Sage 1000 (and 500\) and Sage 200\.  In particular, Codis has provided the Excelerator software that provides two\-way integration between Sage and Excel.

Sage 500/1000 did not provide any API for years, and when was provided, it was not suitable for use by integration products like Excelerator.  Business rules and data updates were derived using experience and examining data updates.  S200 has an API that provides a lot but not all the business rules required.

The products we sell and support are described here: [Codis Product Guide.aspx](Codis Product Guide.md) and some information about the different ways those products are deployed is described here:[Codis Software Deployment Configurations.aspx](Excelerator Deployment Configurations.md)

# Excelerator Architectural History

Excelerator had 3 distinct phases in its architectural history: 

- VB V1 \- almost all code was developed in Visual Basic with very small amount of code in C\+\+.  All software was for integrating with Sage 1000 and it was deployed only to the client.  When Excelerator was first written, VB provided the easiest and clearest way to integrate with Excel.  VB compiled into COM components.  As not all modules have been ported from VB V1 into V3, V1 remains deployed on some sites.
- .Net V1 \- a hybrid .net/VB solution. Client\-server software that used WCF to communicate between client and server software.  VB.Net chosen to allow an easier migration. The server software still used the VB COM components (with .net wrappers), as these contains business rules that had taken years to derive.  All software was still for intergating with Sage 1000\.  Server side WCF services are also sold separately for interfacing with 3rd party products.
- V3 (.net) \- pure .net code with significant enhancements to the Excel Excelerator UI and APIs for simplifying the Excel interface.  V3 products integrate with both Sage 200 and Sage 1000\.  See also [Codis Excelerator V3\.aspx](Codis Excelerator V3.md)

Other changes that had a significant impact on the architecture include:

- Adoptation of Spring.net.  [Codis Development Framework \- IOC Spring\-Net.aspx](Codis Development Framework - IOC Spring.Net.md).
- Sage 200 Cloud/2015\.  This term has to be used with care as Sage have frequently changed the terminolgy in this area, and the term "Cloud" is more recently used to refer to non\-cloud solutions.  However, in Sage 200 2015 Sage released a version that allowed the server components to be placed on a cloud server.  Codis accommodated this change but it placed significant limitations on our code in some areas: [https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Cloud%20Excelerator%20Architecture%20and%20Coding%20Guidelines.aspx](Sage 200 Cloud Excelerator Architecture and Coding Guidelines.md).
- Adoption of TFS/VSTS/AzureDevops.
