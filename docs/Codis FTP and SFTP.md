---
title: Codis FTP and SFTP
tags:
- FTP
- Support
- SFTP
description: FTP allows us to share larger files with external parties. SFTP is known
  as Secure Ftp and is a more secure method of transferring large files.…
created: '2017-01-24'
modified: '2023-04-21'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20FTP%20and%20SFTP.aspx
---

FTP allows us to share larger files with external parties. SFTP is known as Secure Ftp and is a more secure method of transferring large files. 

## Upload files to FTP

### Connect to FTP

**Please access through below respective One Drive locations \- Backend (Internal Use Only)**

[Marketing](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Marketing?csf=1&e=JlGvQf)

[Sales](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Sales?csf=1&e=tYjisL)

[Prerelease](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Prerelease?csf=1&e=hqR71f)

[Release](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Release?csf=1&e=eOQSqf)

[General](https://codislimited-my.sharepoint.com/personal/codis_support_codis_co_uk/_layouts/15/onedrive.aspx?csf=1&e=tYjisL&cid=f25b616a-2b7e-4391-bd24-943d90179844&FolderCTID=0x0120002EEA93101B7C8C48B0EF7E3922E45E36&id=/personal/codis_support_codis_co_uk/Documents/FTP/General)  

**If you are accessing remotely from Customer's Site and you want to upload their data, use below link \- Frontend**   
[ftp://codisftp.codis.co.uk](ftp://codisftp.codis.co.uk/)

### 

### Login as Manager (required for upload)

![](images/Support_Support_Wiki_Images_FTP_FTP_Login.png) 

### Open FTP with Windows Explorer

Open Windows Explorer and then type the FTP site in the address bar. If it prompts for username and password use **CodisFtpManager** credentials.

![](images/Support_Support_Wiki_Images_FTP_Open_With_Windows_Explorer.JPG) 

Open the respective folder where you want to upload the data, then copy and paste the files into your FTP folder. 

## Download files from FTP

### Connect to FTP

**Please access through below respective One Drive locations \- Backend (Internal Use Only)**

[Marketing](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Marketing?csf=1&e=JlGvQf)

[Sales](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Sales?csf=1&e=tYjisL)

[Prerelease](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Prerelease?csf=1&e=hqR71f)

[Release](https://codislimited-my.sharepoint.com/:f:/r/personal/codis_support_codis_co_uk/Documents/FTP/Release?csf=1&e=eOQSqf)

[General](https://codislimited-my.sharepoint.com/personal/codis_support_codis_co_uk/_layouts/15/onedrive.aspx?csf=1&e=tYjisL&cid=f25b616a-2b7e-4391-bd24-943d90179844&FolderCTID=0x0120002EEA93101B7C8C48B0EF7E3922E45E36&id=/personal/codis_support_codis_co_uk/Documents/FTP/General)  

**If you are accessing remotely use below link \- Frontend (For customers with below credentials)**  
[ftp://codisftp.codis.co.uk](ftp://codisftp.codis.co.uk/)

### Login as User (required for download)

![](images/Support_Support_Wiki_Images_FTP_FTP_Login.png)  

### Codis FTP External Parties \- Quick guide (Filezilla):

The end user procedure is detailed in [How to download files from Codis FTP using FileZilla](https://codislimited.sharepoint.com/sites/Wiki/Support/Support%20Wiki/Documents/FTP/How%20to%20download%20files%20from%20Codis%20FTP%20using%20FileZilla.pdf) . 

## Sending FTP Download Link to Customers

### Generate a FTP link to the file

First of all we have to get a copy of the link. Open the folder in ftp view logging in as above CodisFtpUser, navigate to the file you need to send to customer, right click and select Copy shortcut.

 ![](images/Sales_Sales_Wiki_Images_Codis_FTP_Screenshot.PNG.PNG)

We can then use this link as a hyperlink in an email.  

Once the user clicks they will have to sign in with **CodisFtpUser** to download the file.

### 

## Secure FTP

We also use Secure FTP logins for customers. A secure FTP login will have to be created for the customer. The login will be created by the IT Manager. 

**IMPORTANT: It is highly important to note that for any customer data \- only Secure FTP should be used. Customer data should never be copied or uploaded to FTP. SFTP should always be used in this instance. If there is any confusion with regards to this then please speak to management for further clarification.** 

The details for this are as below: 

Backend (For Codis Internal Use Only): Look for the folder name of the respective company's SFTP Username.  

[**\\\\CD01NSSY001\\Homes**](file://///cd01nssy001/Homes)

Frontend (For Client / Customer):\- 

**Host Name: sftp.codis.co.uk or Host IP Address: 81\.150\.164\.4**

**SFTP Port: 22** 

Username: specific to customer and created when SFTP details are created for the customer 

Password: specific to customer and created when SFTP details are created for the customer 

A small FTP client software may have to be downloaded and installed from [this](https://filezilla-project.org/download.php?show_all=1) link . 

### Secure FTP External Parties \- Quick guide (Filezilla):

A quick guide on how to upload \& download files on Codis Secure FTP can be accessed by [clicking here](https://codislimited.sharepoint.com/sites/Wiki/Support/Support%20Wiki/Documents/FTP/How%20to%20upload%20%26%20download%20files%20on%20Codis%20Secure%20FTP.pdf)
