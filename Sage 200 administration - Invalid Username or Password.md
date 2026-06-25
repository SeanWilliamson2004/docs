---
title: Sage 200 administration - Invalid Username or Password
tags: []
description: This is the error this could be because of API being enabled in Sage
  200 administration. if they want to use it then they can either upgrade to a new…
created: '2021-10-18'
modified: '2021-10-18'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20administration%20-%20Invalid%20Username%20or%20Password.aspx
---

![invalid user.png](images/PublishingImages_Pages_Sage_200_administration_-_Invalid_Username_or_Password_invalid_user.png)  


This is the error  


  


this could be because of API being enabled in Sage 200 administration.  


if they want to use it then they can either upgrade to a new version of Sage or follow the below to disable the api from backend  


open SQL management studio and do the following query  


  



```
--delete the entry to the API
DELETE FROM tblParameters where ParameterName = 'APISiteID'

--delete API user entries
DELETE FROM tblExtIdentity where ExtIdentityTypeID IN (1,2)

--remove any API references to existing users
UPDATE tblUser
SET isAPIUser = 0
WHERE isAPIUser = 1  

```
