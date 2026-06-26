---
title: codis bi test page
tags: []
description: 'Pre-requisites: Communicate to Customer to get the Form filled. Codis
  BI Form.xlsx Now count the number of "Yes" we got in the form and match that…'
created: '2022-11-22'
modified: '2022-11-22'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/codis%20bi%20test%20page.aspx
---

# Pre\-requisites:

- Communicate to Customer to get the Form filled.  
*\[image: clip\_image001\.png not found]*[Codis BI Form.xlsx](https://codislimited.sharepoint.com/sites/Wiki/Support/Support%20Wiki/PowerBI/Documents/Codis%20BI%20Form.xlsx)
- Now count the number of "Yes" we got in the form and match that number to the "allowed users" number on CRM. And to get the allowed number of users:
- Go to CRM open Customer company\>Licences\>Enterprise. And then type "PBI" to search relevant Licences.  
![Pre requisite Licence snap](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Screenshot_20221121_173709.png)
- Then we can get the Number of Allowed Users.
- Do not amend that number without "Accounts dept." affirmation.

1\)     **Log in to CRM on****your PC.**

2\)     Search for Company (e.g., Alphasites)

3\)     Go to**Licences.**

4\)     First **check**that they have the required **Licences:**

1. Click on Enterprise Licences
2. Look for anything with Power BI in it, its product code must contain **"PBI"**
3. Check if there is at least one allowed user
4. Check if the Expiry date is Valid.  
![4.4 Licence validity check](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Screenshot_20221121_173112.png)
5. If both or any one of the above steps gives a negative result, then **Don't amend** them  
but can be talked to **"Accounts dept."** about it. Because Customer might not have paid for it.

5\)     Then generate a **Recovery key** which will be required later.

1. Go to **your PC** and search for "generate secure password" on any  
search engine e.g., google.com, and visit any website to generate a password.
2. Use at least 20 characters and must include "Uppercase", Lowercase",  
"Numbers", "Symbols".
3. Copy that password and save it on CRM, under ASI tab of that company, as  
"Data Gateway Recovery Key", in Notes section.

6\)     **Go to powerbi.com** on **your PC**.

1. Create a **Workspace** for the company before login to their server.  
Click on Workspaces\>Create a workspace.  
![6.1 Create Workspace](images/Support_Support_Wiki_PowerBI_Images_Screenshot_20221121_170223.png)  
  
![6.1 Create workspace 2](images/PublishingImages_Pages_Codis_BI_Installation_Steps_with_Snaps_Screenshot_20221121_170407.png)
2. Now in that workspace Click on "Access" to add a Group named as "**AllSupport**"  
and make it Admin and Click on Add.  
![6.2 Accessing Access setting](images/PublishingImages_Pages_Codis_BI_Installation_Steps_with_Snaps_Screenshot_20221121_170603.png)  
![6.2 Acessing access setting 2](images/PublishingImages_Pages_Codis_BI_Installation_Steps_with_Snaps_Screenshot_20221121_170704.png)
3. Now everyone else at Codis can manage this workspace too, which are in that group.

7\)     **Go to Power BI Desktop on****your PC.**

1. Now **Publish** the report of that company to respective workspace.  
![7.1 Publish to workspace](images/PublishingImages_Pages_Codis_BI_Installation_Steps_with_Snaps_Screenshot_20221121_170845.png)
2. And if the Customer have bought a multiple number of Dashboards,  
then publish all of them to their company named workspace.
3. After then, go to powerbi.com \& check if all the customer's dashboards are present there in  
customer's workspace.  
![7.3 report list on workspace](images/PublishingImages_Pages_Codis_BI_Installation_Steps_with_Snaps_Screenshot_20221121_171056.png)

***8\)***    ***Now all the preparations have been made before going into the customer Machine.***

  


9\)     **Log on to Customer Server** preferably by TeamViewer,  
but after checking some things mentioned below.  


1. When you log in to their server, their IT person will be watching, that IT person must  
be added to the CRM under their company's people tab and that person must  
be **License Administrator**, and that **person email** must be correct.
2. If that person is not in the list there, then add him by clicking on "New Person", then  
Tick on Licence Administrator and Save it, then Click on Email, add Email and Save it.
3. And if that person is added but fields are not correct then correct them by clicking on that  
person's name and go to "Change" and then follow onscreen accordingly.

10\)  Go to the link to download Codis Power BI Installer File.  
https://downloads.codis.co.uk/Codis/PowerBI/CodisPowerBIInstaller.exe  
  
Click on More info\>Run anyway  
![10 Run anyway](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Screenshot_2022-11-21_134129.png)  
![10 Run anyway 2](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Screenshot_2022-11-21_134226.png)  


11\)  Then Right click and select "Run as administrator".

12\)  After then it might ask the administrator to log in.

13\)  Then the IT person may do the needful.

14\)  And it will say  
*"Installation Successful. Opening Licence Registration and Gateway*  
*download. Press any key to exit…"*

15\)  Then it will open**Licence Program.** Or it can also be opened by following this path.  


16\)  (C:) \> Program files \> Codis BI \> Licences \> Licences.exe  
![16 Licence Program.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Licence_Program.PNG)  
  
  
 

17\)  **Then register the server for Licence**.

1. Click on Register Now\>next\>Log in.
2. Now **there IT will Login** using the Email ID which is Licence administrator,  
that could be Company Email or Gmail, select accordingly.  
![17.2 Select IT log in.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Select_IT_log_in.PNG)
3. Then it will ask to close the tab.  
![17.3 close the tab.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_close_the_tab.PNG)
4. Then on Licence program it will say "Finished".  
![17.4 Licence reg finish.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Licence_reg_finish.PNG)
5. Click Finish to Exit.

18\)  Then it will show the list of couple of products.  
![18 List of products.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_List_of_products.PNG)  


19\)  Click on refresh once. It should say Licence Refreshed Successful.  


20\)  It will give an Error  
*"The Licence for Codis Integrated Platform has expired. Contact your IT administrator".*  
You can ignore that error.   


21\)  Before moving forward, **check** one more thing.

1. That there is **at least one user** with power BI Licence in the product list  
which has **valid expiry date**.
2. And that product code must contain **"PBI",**Otherwise, Web Service would not work.
3. And now close the Licence window.

**22\)** **Gateway Installation:**

1. This url should already be open on the customer's server. If not then navigate to it: [https://www.microsoft.com/en\-us/download/details.aspx?id\=53127](https://www.microsoft.com/en-us/download/details.aspx?id=53127)  
![22.1 data gateway download.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_gateway_download.PNG)
2. Download
3. Open "GatewayInstallation.exe", which got downloaded
4. **Install On\-premises Data Gateway.  
![22.4 gateway installation screen 1.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_gateway_installation_screen_1.PNG)**

23\)  Now after installation it will ask the Email address.

24\)  Here **log in using our Codis Email Address**. Because we are  
managing data gateway for them.  
![24 Codis Email data gateway.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Codis_Email_data_gateway.PNG)  
![24b Microsoft_Azure_gateway.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Microsoft_Azure_gateway.PNG)  
  


25\)  Now, when prompted, use the first option, which is: *Register a new gateway on this computer*.  


![25 Register a new gateway.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Register_a_new_gateway.PNG)  


26\)  Now *"New On\-premises data gateway name"* is their **Company name**, it must be the **exact match**to the company name entered on **CRM**.  
![26 Data Gateway Name.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Data_Gateway_Name.PNG)  


27\)  Use the **Recovery key** which was generated in step 5\.

28\)  And if IT asks for that key then give it to them as well.

29\)  Click on Configure.

30\)  Then it will say *"the Gateway for the respected company is online and ready to be used".  
![30 Gateway is online.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Gateway_is_online.PNG)*

31\)  Then Close it.  
  
 

**32\)** Final Check on customer server before starting ***Configurations*****:**

1. Open this URL: [http://localhost:26061/](http://localhost:26061/)
2. It should say the service is Running.  
![32.2 Gateway service is running.PNG](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Gateway_service_is_running.PNG)

33\)  Now **link the Gateway** that just got Installed to the Datasets, published in step 6\.

1. **Go to powerbi.com on****your PC**
2. Go to the workspace created for the customer.  
![33.2 Workspace after installation.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Workspace_after_installation.png)
3. Go to the settings\>Manage Gateway.  
![33.3 settings and manage gateway.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_settings_and_manage_gateway.png)
4. Go to *"On\-premises data gateway"*tab.  
![33.4 onpremise data gateway tab.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_onpremise_data_gateway_tab.png)
5. Then hit *refresh icon* present under status for all gateway clusters present there.  
![33.5 refresh icon under status.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_refresh_icon_under_status.png)
6. Check which one is online.
7. Click on 3 dots next to Gateway name\>Manage Users.
8. Select "**AllSupport**" Group, Select Admin, Then Click on Share.  
![33.8 data gateway users admin.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_gateway_users_admin.png)
9. Click on 3 dots next to Gateway name\>Settings.  
![33.9 data gateway settings open.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_gateway_settings_open.png)
10. Go to Power BI section and Tick mark both the check boxes.  
![33.10 data gateway settings.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_gateway_settings.png)

34\)  Now **Configuring Data Sources**.

1. Go to settings\>Manage Gateway  
![34.1 settings and manage gateway.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_settings_and_manage_gateway.png)
2. Go to "Data Sources".  
![34.2 New data source click.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_New_data_source_click.png)
3. Click on "\+ New" on top left corner, to Add new Data Source.
4. Now fill these **details**:
1. Gateway Cluster Name \-\> Company Name exactly same as in CRM
2. Data Source Name \-\> Company Name – "Codis BI Web Service"
3. Data Source Type \-\> Web
4. URL \-\> [http://localhost:26061/](http://localhost:26061/)
5. Authentication method \-\> Anonymous
6. Privacy level \-\> Organisational  
![34.4.6 New data source fill details.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_New_data_source_fill_details.png)

6. Click on Create. And close that.
7. Then go to listed Data source which we created and hit refresh icon under status.  
It should show online.  
![34.6 Data Source refresh icon under status.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Data_Source_refresh_icon_under_status.png)

35\)  Now go to 3 dots next to Data source we just created, which must be listed under "Data Sources".

1. Search for "AllSupport", select it and mark "Owner".  
![35.1 Data source users selection.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Data_source_users_selection.png)
2. Then Click on Share.

36\)  Go to **Data sets on workspace.**

1. Click on 3 dots next to Dataset\>Settings.  
![36.1 data sets settings.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_sets_settings.png)
2. Then go to Gateway connections.
3. Now because Data Sources for our data gateway are configured,  
it must show green tick mark right before the Web URL.
4. Then Click on Drop down and select the Data Source Name you gave in step 34\.  
![36.4 data gateway in data set settings mapping.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_data_gateway_in_data_set_settings_mapping.png)
5. Then hit Apply.

37\)  Putting **Databases names as Parameter**.  


1. Open Parameters, which is available on the same page.
2. Put Databases Names comma separated without spaces. Which we must have  
got from customer before this session in the Form.  
![37.2 Parameter Names filled.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Parameter_Names_filled.png)

38\)  **Check if Refreshing dataset works**.  
**Note**: Sometimes, it may need**1 day** to get refreshed without errors.

1. Go to Customer workspace and click on dataset.  
![38.1 Refresh.png](images/PublishingImages_Pages_Codis_BI_Installation_Steps_Refresh.png)
2. Hit refresh, it should not show error, check it. It will show refresh date and time if it gets refreshed successfully.

39\)  **Then Schedule Refresh**.

1. Got to Dataset 3 dots\>settings.
2. Then open Schedule Refresh. And configure it.

40\)  Now Before Logging off from Customer, we can use URL on the customers server to  
check the web service is working. (Put correct Databases Names in the URL  
as comma separated without spaces)  
[http://localhost:26061/table?tableName\=SYSCompany\&databases\=Test,Demo](http://localhost:26061/table?tableName=SYSCompany&databases=KnDemo)

41\)  Also Before logging off from Customer, Delete Both Installation files.

42\)  Now **Create an App**.

1. Go to Powerbi.com\>Customer workspace\>Create App
2. Fill these details:
1. App Name \-\> \[Company Name]
2. Description \-\> Reports for \[Company Name]
3. App Logo \-\> *\[image: clip\_image001\.gif not found]*[Codis Logo Transparent.png](https://codislimited.sharepoint.com/sites/Wiki/Support/Support%20Wiki/PowerBI/Images/Codis%20Logo%20Transparent.png)
4. Contact Information \-\> Show specific individuals or groups \-\> "Codis Support"
5. Global App Settings \-\> Leave Unticked all
6. Support Site \-\> [https://help.codis.co.uk](https://help.codis.co.uk/)

4. Click on "Next: App content"
5. Click on "\+Add Content"
6. Select all reports\>Add
7. Click "Next: Add audience"
8. Manage Audience access\>Grant access to\>Specific users or groups
9. Then copy and paste here, the emails from the Form, which was filled by the customer before the session. Add Emails according to the role and report. Also don't add emails to the report which don't have any roles assigned in the form for that report.

43\)  Then click on **Publish App**. Then it will provide the Link.

44\)  That Link can be sent to the customer to view the reports once row level securities are configured.

**45\)** **Configuring the Row Level Security**

1. Go to powerbi.com
2. Go to dataset in workspace of that company.
3. Click on 3 dots\>Security
4. Paste the Email addresses in respective roles, which we got from the customer in the form before the session.  
(The respective Role names should exactly match to the Form)  
Also don't add emails which don't have any roles assigned in the form.
