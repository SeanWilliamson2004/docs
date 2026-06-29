---
title: Sage 200 Power BI notes
tags: []
description: For installation see here . You need to be acquainted with the Sage 200
  api, docs are here:…
created: '2022-05-20'
modified: '2022-05-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Power%20BI%20notes.aspx
---

For installation see [here](Sage 200 - Power BI.md).   

You need to be acquainted with the Sage 200 api, docs are here:[https://developer.columbus.sage.com/docs\#/uk/sage200/accounts/gs\-welcome](https://developer.columbus.sage.com/docs#/uk/sage200/accounts/gs-welcome)  

\- Company Name is a parameter in M, populated by a drop down box\- In "manage parameters" from the power query editor, you can populate the drop down box using a query. The query used here is Sage200\.GetSites(null) which just returns the list of companies.\- So at minimum to create a new dashboard we need to copy the following from the sample dashboard sage provide:  \- Company Name parameter  \- Companies table  \- API Query  \- Feed  
\- The connector gets the data in chunks of 5000\. Could this be why it's so slow? 80k customers means 16 http requests.  
\- Each api request requires these headers:1. X\-Site: The connector sends this automatically by getting the first site that has a company name matching the Company Name parameter
2. X\-Company: The Company Name parameter
3. ocp\-apim\-subscription\-key: This is in the config file within the power BI connector file (need to convert it to zip first then open it up to see it). It is why you need to download the connector from the Sage 200 desktop app first
4. Authorization: The bearer token retrieved at the start on login to the microsoft account

\- the "select" query parameter still returns those columns, but the column values will be null. So we need to then remove those columns in power bi.
