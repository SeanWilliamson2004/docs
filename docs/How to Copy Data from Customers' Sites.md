---
title: How to Copy Data from Customers' Sites
tags: []
description: Purpose This process avoids customer data being stored on local PCs altogether.
  Instead, it creates a single, central copy that can be accessed as…
created: '2026-04-14'
modified: '2026-04-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/How%20to%20Copy%20Data%20from%20Customers'%20Sites.aspx
---

## Purpose

 This process avoids customer data being stored on local PCs altogether. Instead, it creates a single, central copy that can be accessed as required to restore data to the customer’s Sage server. 

 While this may appear to introduce an unnecessary additional copy of the data, it provides two key benefits: 

- Any temporary copies created during the restore process can be deleted immediately once the restore is complete.
- It provides an auditable record of why and when the data was used, stored alongside the data itself.

## Procedure

### 1\. Access the shared folder

- If you do not already have access, request a link to the shared 

 **CustomersData** folder in OneDrive.
- Open the link in OneDrive and select 

 **“Add shortcut to My files”**.
- After a short delay, the folder will appear in File Explorer.

### 2\. Create a dedicated folder

- Within **CustomersData**, create a new folder specifically

 for the dataset being transferred.
- Add a `README.md` file to this folder explaining why the data

 is required (for example, a case or ticket number).

### 3\. Transfer the data

- Use TeamViewer file transfer to copy the files directly into the newly

 created folder.
- The shared **CustomersData** folder should appear under

 *Local Computer* in File Explorer, typically at:

```
C:\Users\<username>

e.g. C:\Users\Sean.Williamson


```
### 4\. Restore the data

- Copy the data from this folder to the customer’s Sage server and perform

 the restore.
- Delete all `.bak` files created during this process once the

 restore is complete.

### 5\. Clean up

- When the data is no longer required, delete the copy in OneDrive.
- Delete the restored database on the Sage server.
