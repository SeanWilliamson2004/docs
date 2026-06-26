---
title: Online Licensing Enterprise - Developer's Notes
tags:
- Development
- Online
- Licensing
- Enterprise
description: This is a collection of notes made to help developers license Enterprise.
  It relates to the test CRM system and Prerelease Codis IP. We have released…
created: '2017-01-28'
modified: '2017-01-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Online%20Licensing%20Enterprise%20-%20Developer's%20Notes.aspx
---

**This is a collection of notes made to help developers license Enterprise. It relates to the test CRM system and Prerelease Codis IP.** 

We have released to source safe in late August new Online licensing functionality. This was done with the assumption that the corresponding functionality in CRM was to go live soon after. This didn't happen and is currently scheduled to happen in late November. 

[Instructions for licensing a customer that needs patching so has to use the new Codis IP Licensing](Online Licensing System.md)

We also need to licence our own development PCs. 

The licensing system tracks which individual servers and their characteristics and ties them to a customer and the products that the customer has bought. Because individual developers might work with new or different products, each developer/PC has to create and use their own company in CRM to track their licences. This is covered in the notes linked to above. 

To create a new company and licence: 

1. Create the company in CRM entering the mandatory data
2. Mark the company as a test company
3. Select the Licences tab
4. Select Enterprise
5. Set the company to allow Online (and offline) licences. The only way I could find to do this was to add a dummy server Servers\-\>Add Server (using a made up computer ID). Then select that server in the left list and select "Edit Summary". Select "Online" as the Version, then tick "Allow Offline Licences" and save.
6. Add the IP Users product. Licences\-\>Add Product \-\> add C1000IPLUSPR \-\> Save
7. Renew the IP Users product. Select the C1000IPLUSPR product in the Left list and and click on "Renew". Change the Expiry date to be a date in the future, enter a dummy invoice number and save.
8. Add users to the IP Users product. Select the C1000IPLUSPR product in the Left list and Adjust Total Users (on right) to e.g.10\. Enter a dummy invoice number and save
9. Repeat the last 3 steps for modules like E1000NLJENPR. (You can search in the product entry box). (You must renew and add users for each module too.)

Then run Codis.System as described in the linked to video and follow the instructions to licence an offline server. 

If you make a mistake or have to change your licence, at the moment the only way to change an offline licence is to delete the CodisLicence file in C:\\ProgramData\\Codis\\Licence and then re\-register
