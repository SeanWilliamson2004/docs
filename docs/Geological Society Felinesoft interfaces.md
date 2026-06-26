---
title: Geological Society Felinesoft interfaces
tags:
- Interfaces
description: These interfaces have been superceeded by new interfaces to a new CRM
  system . The Geological Society commissioned Felinesoft (a 3rd party company)…
created: '2023-05-17'
modified: '2025-08-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Geological%20Society%20Felinesoft%20interfaces.aspx
---

These interfaces have been superceeded by [new interfaces to a new CRM system](Geological Society CRM Interfaces.md).  
  
The Geological Society commissioned Felinesoft (a 3rd party company) to supply a new CRM system based on MS Dynamics.  Codis joined the project to port their Sage 500 system to Sage 200 and produce new interfaces between the old Care CRM system and Sage 200, and then between the new Felinesoft CRM system and Sage 200\.  


Due to difficulties between Felinesoft and GeoSoc, this project did not complete as we would have liked.  Felinesoft withdrew from the entire project leaving their side of the interfaces unmaintained (this may have changed?).  The interfaces are used but supported on a best endeavours basis.    


  


There is no reliable document that describes the interfaces.  The closest is probably [https://codislimited.sharepoint.com/:u:/r/sites/pwa/Geological%20Society%20S200%20Upgrade/\_layouts/15/Doc.aspx?sourcedoc\=%7B546EEF18\-70CD\-4DA7\-B46C\-7AE863F000DC%7D\&file\=CodisGeoSocGLToOrders.vsdx\&action\=default](/:u:/r/sites/pwa/Geological%20Society%20S200%20Upgrade/_layouts/15/Doc.aspx?sourcedoc=%7b546EEF18-70CD-4DA7-B46C-7AE863F000DC%7d&file=CodisGeoSocGLToOrders.vsdx&action=default) but this prepared by us but was not acknowledged by either Felinesoft or GeoSoc as a master.  This [https://codislimited.sharepoint.com/:u:/s/pwa/Geological%20Society%20S200%20Upgrade/EXMI\_z\_roRRFj\_k7iliiKGwBr\-GjiNUDcJspm7DnasxAKw](/:u:/s/pwa/Geological%20Society%20S200%20Upgrade/EXMI_z_roRRFj_k7iliiKGwBr-GjiNUDcJspm7DnasxAKw) can be useful as it was a Felinesoft document and it does describe some of the different processes that need to be supported. 

 All interfaces are WCF SOAP. 

  


There is a test client in Repos\\CodisDevelopment\\Sage200\\Server\\Enterprise\\Codis.WCF.Sage200Enterprise\\CodisWebserviceSample\\. 

  


WCF message tracing is enabled on the GeoSoc UAT server.  The traces are saved to different locations but all within the c:\\codislog folder.  The traces can grow to be unmanageable fairly quickly.  (It would be good to have a log gile size\-based rollover mechanism, but I've never had a chance to set it up, partly because it is difficult to tell if you've broken the logging as there is always a lag in saving.) 

SvcTraceViewer.exe is in the codislog folder.   


Tracing is essential as it allows the full request to be retrieved for an error.  The error given to us by FelineSoft or Geosoc will usually have the Entity ID.  Filtering on this will give the relevant messages.  Exceptions can also be picked out, and the full stack trace retrieved.   


The interfaces have introduced demands to track additional data not required for Excelerator \- source record identifiers.  

For instance, Customers are created by generating the Sage customer ID, which is fed back to the source system.  But a connection\-less system like this one is vulnerable to transmission failures, and a customer may be generated and the result not fed back to Sage.  By including a source ID in the message sent to create a customer \- a unique identifier known to the source system \- and storing this against the customer in Sage, the interface can recognise that this customer has already been created.   

To accommodate this, we have added custom tables.   The supporting files for these are in the S200SupportingFiles Repo. 

   


Added 17\.05\.23 by SW 

   


## Interfaces Used (as best as we can recall)

### Codis.Sage200\.Stock.Server.StockAPIServer

GetLastUpdatedProducts 

GetLastUpdatedStock 

GetNominalCodes() As List(Of NominalAccountBrowseDTO) 

Function GetCostCentres() As List(Of CodeAndNameDTO) 

Function GetDepartments() As List(Of CodeAndNameDTO) 

### Codis.Sage200\.SalesOrder.Server.SalesOrderServerAPI

Save 

   


### Codis.Sage200\.SOPInvoice.Server

All services 

### Codis.Sage200\.OrderPaymentAllocation.Server

All services 

### Codis.Sage200\.Customers.Server.CustomerServerAPI

Save
