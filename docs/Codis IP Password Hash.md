---
title: Codis IP Password Hash
tags: []
description: Hashing a password is one way transaformation on a password. Hash password
  can not be turned back into the original password. We have introduced a…
created: '2021-09-17'
modified: '2022-03-29'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20IP%20Password%20Hash.aspx
---

Hashing a password is one way transaformation on a password. Hash password can not be turned back into the original password.

We have introduced a hash password utility application to change the codis ip user password to hash. In Codis IP web application rather than enrypting and decrypting user password we store the user password in hash. On user login the entered password is converted into hash and compare with stored user hash password for verification. Hash password processing is used in changing user password.  

Use this link to download application and click the file named "Codis.IP.PasswordHashUtility.UI.exe" to launch application  

NOTE: For Password Hashing feature, this Utility creates the Salt field in SecurityUsers table automatically if not present.

https://dev.azure.com/codislimited/CodisDevelopment/\_build/results?buildId\=14490\&view\=artifacts\&pathAsName\=false\&type\=publishedArtifacts

1\)Open the application by clicking it and you will see 

       ![App1.PNG](images/PublishingImages_Pages_Codis_IP_Password_Hash_App1.PNG)

2\)Click on either All or Single radio button. On choosing the "All" changes the password of all users in codis ip.

3\)On choosing "Single " changes the password for specifed user only.   

    ![App2.PNG](images/PublishingImages_Pages_Codis_IP_Password_Hash_App2.PNG)
