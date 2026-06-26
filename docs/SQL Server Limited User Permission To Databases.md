---
title: SQL Server Limited User Permission To Databases
tags:
- Support
- SQL
description: Configuring non-administrator users to access SQL How to set up windows
  users to have limited access to MS SQL files Where and why this is useful…
created: '2017-01-27'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/SQL%20Server%20Limited%20User%20Permission%20To%20Databases.aspx
---

**Configuring non\-administrator users to access SQL** How to set up windows users to have limited access to MS SQL files 

## Where and why this is useful

### Excel Views

Allows users to access SQL views or queries without administrator privileges 

### SQL Backups from Command Line

Allows users to backup SQL databases from the command line. Do not need to run Management studio. A batch file can contain the following line.   
sqlcmd \-e \-s **servername** \-q "Backup database **databasename** to Disk\=**filename**"   
example   
sqlcmd \-e \-s CS200v2015 \-q "Backup database CRM to Disk\='c:\\cmc\\crm.bak'" 

## Configuration

### Configure Windows

#### Configure New Group in windows

#### Add Users to the group

### 

### Configure SQL

#### Create this Group In SQL

#### Configure SQL users to access the database
