---
title: Care Import Program
tags:
- Development
description: This page gives a brief overview of what the "Care Import" program made
  by Codis is “Care” is a membership system that a few of the not-for-profit…
created: '2017-01-23'
modified: '2017-01-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Care%20Import%20Program.aspx
---

**This page gives a brief overview of what the "Care Import" program made by Codis is** 

“Care” is a membership system that a few of the not\-for\-profit customers use. E.g. RSPCA 

Care created interfaces from their software into Sage. Those interfaces are: 

- Sales invoices
- Customers
- NL Journals
- Cash Receipts and Payments

Not all the customers use all the interfaces. 

The interfaces were implemented using Tetralink as an import tool. They were not implemented by somebody who fully understood Tetralink, and the output files files from Care for the transactional imports had multiple nominal codes and values in a single line, to mirror the structure of the underlying tables. (Note: the files are flat text files, space delimited). 

As they were created for a CISAM system, the NL Journal files had up to 30 NL codes (as was the structure in CISAM). This meant it was not possible to create a Tetralink based solution using the existing file format, and Care would not change the structure. (There was also a bug in the import that happened in certain circumstances – I can’t remember the details). 

See the attached file for an example of the file data. 

We decide to create a dedicated program for importing the Care files. This program would consist of: 

1\.       A user interface for picking files to import 2\.       File processing that picked out the data from the data file and presented it to our standard APIs for processing. It also had to move processed files to a selected directory. 3\.       Our standard APIs 

2\. required some way of specifying which data field was where in the text file. (Where is normally specified by an offset). This varied slightly between sites, so it could not be hard coded. In the first release we decided to use the Microsoft ODBC Text driver for this. This driver allowed you to specify field names and offsets in a file called schema.ini. This had a number of weaknesses: 1\.       Schema.ini had to be in the same directory as the import files 2\.       Schema.ini specified the name of the import file. Because of this import files had to be temporarily renamed to the file name specified in schema.ini. This could cause problems if the import failed. 3\.       Schema.ini was awkward to specify. Offsets had to be from the previous field rather than absolute. 4\.       MDAC 2\.? that was introduced with Windows XP SP2 (amongst other OS versions) introduced a bug into MS ODBC Text driver. (See old RSPCA logs) 

4\) proved a killer for that solution, and we introduced our own text driver that uses an XML file to specify the field names and the offsets.
