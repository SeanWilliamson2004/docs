---
title: Restore SQL .bacpac database and convert to .bak
tags:
- Microsoft
- SQL
- Support
description: Open SQL Server Management Studio (SQL Server Management Studio v17.9.1
  example shown below). Right-click on Databases and select Import Data-tier…
created: '2023-03-01'
modified: '2023-03-01'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Restore%20SQL%20Bacpac%20database%20and%20convert%20to%20Bak.aspx
---

1. Open SQL Server Management Studio (SQL Server Management Studio v17\.9\.1 example shown below).  
 Right\-click on Databases and select **Import Data\-tier Application**.  
![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture1.png)  
  
You will see the below screen. Now, click Next.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture2.png)
2. Click on Browse and select the. bacpac file you downloaded from Azure in the previous step and click Next as shown below –  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture3.png)
3. Here you can change the database name or can keep the same name as the .bacpac file. You can leave the other settings as it is and just click Next again.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture4.png)
4. Verify all the settings below and click Finish or click Previous and go back to the previous settings if you want to change anything.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture5.png)
5. You will see the progress and once it is finished, you will see the below Operation Complete screen. If there is any error, you can click on that and see what is wrong, else you will get all Success  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture6.png)
6. You can see the newly restored database under the Databases folder.  
 **Note:** If you just want to restore the .bacpac database then its all done now, and you can skip the remaining steps.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture7.png)
7. The next step is to create the **.bak** file.  
 For this, right\-click on the new DB and select Tasks \-\> Back Up… as shown below –  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture8.png)
8. Now, you will see the below screen.  
 Remove the destination path that is pre\-selected by clicking Remove as shown below.  
 And then click on Add to select the path where you want to store your .bak file.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture9.png)
9. After clicking on Add, you will see the screen below.  
 Select the destination path/folder and add the desired File name. I have added TestDB12072019\.  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture10.png)
10. Click OK and you will see it executing. Once 100% completed, you will see the following screen –  
 ![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture11.png)  
  
Thats's it! You have created SQL Server .bak file from Azure database .bacpac file.  
![](images/Support_Support_Wiki_Images_Bacpac_to_Bak_Picture12.png)
