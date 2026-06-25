---
title: Release Notes
tags: []
description: We produce release notes detailing changes in our software. Currently,
  only Sage 200 Excelerator has release notes generated. The release notes can…
created: '2022-09-11'
modified: '2022-09-12'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Release%20Notes.aspx
---

We produce release notes detailing changes in our software.  Currently, only Sage 200 Excelerator has release notes generated.  


The release notes can have two purposes:  


1. Internally, we can use them to analyse changes to the software, including to help plan testing.
2. Resellers and customers are informed of enhancements and bug fixes made to the software.

The S200 Release has a task that generates release notes and copies them to the Pre\-Test release folder.    
  
As of release 3\.3\.65, two sets of release notes are generated: External and Internal.  The Internal release notes contain more detail and are intended to help plan testing.  The External notes can be sent to Sales, and Marketing and copied to the Help.  To copy to the help, open the HTML file in SharePoint, and copy the raw HTML.  Then add a new page to the help for the release, edit the HTML and paste.  
  
  
## Technical Notes

For Sage 200 Excelerator, we use [this DevOps extension](https://marketplace.visualstudio.com/items?itemName=richardfennellBM.BM-VSTS-XplatGenerateReleaseNotes) to generate notes.  This:  
- Works out a last completed release based on settings.
- Uses completed PRs since that release to work out associated work items and tests.
- Sends to a [Handlebars.js](https://handlebarsjs.com/) script which generates HTML output using templates that we supply.
- There are two templates  \- one for external, and one for internal.  These are kept in the Codis.BuildComponents repo.

Note: The release notes generator has been configured to look for a completed "Full Release" stage to find the last release.  It doesn't ignore itself, so if the release is completed then the release notes task will no longer generate notes and will overwrite previous notes.  If you need to recreate them because, for instance, work items have been tidied up, then the release ID of the previous release will be needed.  This can be found by running REST API calls listing releases (see ReleaseHistoryReport repo which has a project that can be run, with a debug break, and release info sent to the output).  The Override Build/ Release ID setting on the task should then be set to the ID.  
  


The extension authors provide a helpful tool to aid the design of the templates.  See the notes here: [testconsole](https://github.com/rfennell/AzurePipelines/blob/main/Extensions/XplatGenerateReleaseNotes/V3/testconsole/readme.md).  There are settings files in the Codis.BuildComponents can be used with the testconsole, as well as the templates the release uses.  The testconsole can also be used to regenerate release notes, providing you know the release ID for the release and the previous release.
