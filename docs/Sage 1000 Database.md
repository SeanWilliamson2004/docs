---
title: Sage 1000 Database
tags:
- SQL
- Sage 1000
description: Sage 1000 is an ERP system for medium to large businesses. The data for
  this system is stored in a database. Transferring to a new owner You have…
created: '2017-01-27'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%201000%20Database.aspx
---

**Sage 1000** is an [ERP system](https://en.wikipedia.org/wiki/Enterprise_resource_planning) for medium to large businesses. The data for this system is stored in a database. 

## Transferring to a new owner

You have probably encountered the issue where by the scheme owner can't be assigned rights because there is already a different scheme owner, and have different ways of working around this. You may already know about this, but just in case, this stored procedure will 'repair' the scheme user. You run it against the sage db: 

| ``` 1 ``` | ``` EXEC sp_change_users_login 'Auto_Fix', 'scheme' ``` |
| --- | --- |

You will then just have to grant scheme dbowner rights on the db.
