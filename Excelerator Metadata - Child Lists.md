---
title: Excelerator Metadata - Child Lists
tags:
- Development
- Metadata
- Child
description: This page is aimed at developers only. Overview Transactional data entities
  usually have parent-child relationships. The Codis Framework accommodates…
created: '2017-01-26'
modified: '2017-01-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Metadata%20-%20Child%20Lists.aspx
---

**This page is aimed at developers only.** 

## Overview

Transactional data entities usually have parent\-child relationships. The Codis Framework accommodates this requirement. 

In Excelerator, child list data is entered into separate rows on the spreadsheet \- one for each child list item. (Sometimes the first row of data is entered adjacent to its parent data.) The list is usually open\-ended, apart from Excel or the Finance system limitations. 

In the Codis Framework we generally use light\-weight data transport objects to hold data. A list property can be included on the DTO. Metadata must designate the list properties as being child lists, either through attributes or coded metadata.
