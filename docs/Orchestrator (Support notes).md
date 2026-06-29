---
title: Orchestrator (Support notes)
tags:
- Support
- Orchestrator
description: Overview Orchestrator is Codis software that we use to implement interfaces
  between third party and Sage systems. Interfaces are typically…
created: '2022-03-10'
modified: '2026-01-06'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Orchestrator%20(Support%20notes).aspx
---

# Overview

Orchestrator is Codis software that we use to implement interfaces between third party and Sage systems.   Interfaces are typically implemented between two connectors \- one for the third party system and one for Sage.  The Sage connector will usually be a web service that allows data retrieval and updates.  The third party connector can be a variety of data transports \- usually either messages in files or web services.  Orchestrator sits between these two connectors, coordinating data transfer according to agreed business rules.  

An example of a third party system could be a room booking system that records revenue associated with room bookings.  This revenue has to be recognised in the accounts system for the company using the room booking system.  The room booking system might have a web service that allows retrieval of details of the revenue and this can be used to create Sage accounting journals.  

Note: Orchestrator is named as such because it is an Orchestration engine.  "Data orchestration, at its core, is the process of managing and automating the flow of data across various systems and tools within an organization's data ecosystem."  ([https://www.rudderstack.com/learn/data\-strategy/data\-orchestration/](https://www.rudderstack.com/learn/data-strategy/data-orchestration/)).    Orchestration is usually carried out between endpoints (points of connection) between two systems.  The endpoints are mostly standard and independent of the other system or the Orchestration layer, and it is the Orchestration layer's responsibility to manipulate the data so that the two systems can talk to one another.   As such, an Orchestration layer should not demand changes to the endpoints.  In reality, occasionally some changes are made to 3rd party endpoints, but an integration is more likely to be successful if it does not demand changes to endpoints.  Sometimes, it is simply not possible to change the endpoints.  This demand (to not change endpoints) can shift complexity onto the Orchestration layer.  Another desirable feature of an Orchestrator layer is that it can provide its services a simply as possible and without requiring developer resources.  Adding complexity can push against this demand.  

Orchestrator provides a number of services:  

- Job Scheduling
- Job Logging
- Data transformation
- Data mapping
- Exception management

These are described in more detail below.  

Orchestrator is a framework that provides services and tools to help to implementation of interfaces, but each new interface will require developed coded plugins.    

**Orchestrator has a number of plugins which are designed to process xlsx/csv files based on Excelerator Range definition file. Below is list of Orchestrator plugins which can work with Excelerator Range definition files**  

**Import into Sage 200**  
- Customers
- Invoicing
- NL Journals
- PL Invoice
- PL Payments and allocations
- POP Goods Received/Despatched
- POP Invoice
- Purchase Orders
- Sales Orders
- Suppliers

**Export from Sage 200**  
All export delta information (changes since the last export)  
- Customers
- POP Goods Received Items(GRNs)
- - POP Goods Despatched Items(GRNs Returns)
- NL Codes
- Purchase Orders
- Purchase Returns
- Stocks/Products
- Stock Status
- Suppliers

**Sage 1000**- [PL Invoice](Orchestrator KGH PL Invoice S1000 plugin.md)
# Product Evolution and Phases

## Coded Plugins

There were a couple of assumptions behind the design of this.  

That there are some common tools used for interfaces:  

\* Logging  
\* A secure UI with the capability to configure interfaces  
\* Some basic mapping of data  
\* Scheduled automated processes  

That some interfaces are too complex for some of the tools that are meant to enable interface development, and that coded (by a developer) plugins would be able to meet almost all requirements.  
## CSV Import

This provided a standard plugin for importing CSV Purchase Orders, in a fixed format.   Data mapping is available in Orchestrator.  Any logical automated decisions in data translation will require dedicated coded plugins.  

## CSV Import using Excelerator Range Definitions

This allows a CSV files to be imported based on definitions created using Excelerator Range definitions.  It allows trial and imports of CSV data to be carried out in Excelerator, a template created, then the range definition for the template to be used by Orchestrator to carry out automated imports.   This process provides:  
- A very visible representation of the data transformation and mappings, allowing stakeholders to collaborate in the development of the interface.
- Immediate validation of the result of the data and transformations and mappings.
- Easy entry of 'what\-ifs' to the data to allow the development to continue past errors.
- When live, quick manual correction of invalid imported data whilst the interface beds down.
- Quick transition to an automated solution.
However, one major use case of Excelerator is to use Excel functionality to map and translate data using formula.  Data mapping can be replicated in Orchestrator, but more complex translations that can be carried out in Excelerator will not be possible.  

## CSV Import via a xlsx/xltm/xlsm Excelerator Template

This expands on the previous version, and allows a template to be defined that the CSV file is imported into, then the data is imported from the template into Sage.  Using this approach allows the formula on the template to be used to manipulate the CSV data.  Data can be mapped using, for instance, XLookUp and this mapping can be left for an Orchestrator import.  

Examples of translation rules that can be applied in this version that couldn't in the previous version:  
- Mapping two values into a concatenated value.
- Truncating a value.
- Rules like "If given VAT value \> 0 then Vat Code STD, else Vat Code 0

## Road Mapped Development

### Multi Company Imports

This will match a capability recently introduced into some Excelerator modules that allows it to import to different Sage companies from a single sheet.  

### Excel Data Queries

Add the ability to run parameterised Excel Data Queries from a template.  

# Support Guide:

# [Orchestrator Guide.docx](https://codislimited.sharepoint.com/sites/Wiki/Documents/Orchestrator%20Guide.docx)

# Customer Sites

| **Company** | **Plugin** |
| TWS | Plugin. Uses automation and logging. |
| [Geological Society](Geological Society CRM Interfaces.md) | Excelerator Import, Orchestrator exports |
| KGH | Orchestrator CSV/XLSX Import to Sage 1000 |
| [Mollies \- Tevalis](Mollies Tevalis Integration.md) | Plugin that draws from webservices and manipulates data. |
| [Mollies \- Apaleo](Mollies Apaleo Integration.md) | Plugin that draws from webservices and manipulates data. |
| [Netstock](Netstock CSV Purchase Orders Interface.md) | CSV |
| [Omnes](Help Tipalti-Orchestrator Integrations.md) (Tipalti) | CSV using formula |
| Aggregates R Us (Tipalti) | CSV using formula |
| Fluid Masters (Tipalti) | CSV using formula |
| [Patterson Rothwell](Patterson and Rothwell Interfaces.md) | XLS |
| Resident | Plugin that draws from webservices and manipulates data |

# Deployment

## Architecture

Orchestrator is installed on a server, typically the S200 server.  Details are described here: [Devops Orchestrator README](https://dev.azure.com/codislimited/CodisDevelopment/_git/Orchestrator/README.md)  

For Sage 200 interfaces, usually Sage web services will have to be deployed to the Sage 200 server.  

## Client configurations:

**Mollies**: [Mollies Apaleo Integration.aspx](Mollies Apaleo Integration.md)  
**GeolSoc**: [Orchestrator GeolSoc Integration.aspx](Orchestrator GeolSoc Integration.md)  

## Data Transformation and Data Mapping

Please check this [link](Mollies Apaleo Integration.md#chapter5) from Mollies wiki page to Create/Update/Amend data mappings.  

A third party system may or may not have been set up to provide or receive data that directly matches data accounting system.  For instance \- a room booking is not the same as a journal.  There may be some effort to transform the data within their own system so that the connectors deal in similar or identical concepts.  As part of the transformation, data will normally have to be mapped \- e.g. the third party system has its product code that corresponds to a journal account code.  Again, whether the data is mapped or not varies from interface to interface.  

Data transformation can take place in coding units that Orchestrator loads that are developed by Development.    

Orchestator provides data mapping services that are used by the data transformation services.  The data mapping services are From Value\=\>To Value lists that can be maintained by end users via the Orchestrator front\-end. 

 ![7.Orchestrator FieldMapping.jpg](images/PublishingImages_Pages_Orchestrator_Support_notes_7.Orchestrator_FieldMapping.jpg)  

Data maps are grouped into datasets.  These datasets may correspond directly to obvious concepts in Sage (e.g. customer number) or they might not, depending how the data transformation layer uses them.  This is simply because the data concepts used by the third party system will not allow it.  Data map sets can give the impression that interfaces can be implemented only via configuration of Orchestrator but this is not the case.  The aim of having user configurable datasets is to allow interfaces to be maintained on an on\-going basis by the end\-user without intervention being required by development each time e.g. a new product is added in the third party system.  

## Job Scheduling

Most interfaces have to be run at regular intervals.  Some might poll frequently to see if new data has arrived, and some may run periodically, for instance nightly \- to get a day's transactions.  

Orchestrator includes a job scheduler.  

To create/edit Schedule/Job please follow the below  

- Click on the Scheduled section from User Interface.
- You can select an existing schedule by click on it and click on edit at the right side section on the page under Schedule Details.
- Make changes to the new window which would have existing details of the schedule.
- To Create a new Schedule, click New Schedule button below existing schedules section.
- Enter details in the Text fields and make selections from the dropdown.
- Once you have a schedule with the correct details, click Save to save it.
- You can double check the created schedule by clicking Schedule section again (to reload the page).

Note \- If you click on reload on the browser, it will go to the login page again.  
Note\* \- When the users go live, we setup the mapping after which they would make changes to it and not us.  

![3.Orchestrator SchedulesList.jpg](images/PublishingImages_Pages_Orchestrator_Support_notes_3.Orchestrator_SchedulesList.jpg)  

## Job Logging

Orchestrator provides a framework for the data transformation service to log events, including failures.  

It also provides a front end for the user to view the logged events.  

Click on the 'view log" link next to  status of the run you are looking for and it will open a new window with the log.  

![4.Orchestrator RunHistory.jpg](images/PublishingImages_Pages_Orchestrator_Support_notes_4.Orchestrator_RunHistory.jpg)  

##
