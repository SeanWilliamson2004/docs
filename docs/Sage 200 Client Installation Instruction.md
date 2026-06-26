---
title: Sage 200 Client Installation Instruction
tags:
- Solution
description: Step by step instructions on how to install Sage 200 Client on user's
  pc. Login with Administrative rights - Local and Domain Check the User Account…
created: '2017-03-17'
modified: '2019-12-06'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Client%20Installation%20Instruction%20-%20Old.aspx
---

## Step by step instructions on how to install Sage 200 Client on user's pc.

**Login with Administrative rights \- Local and Domain** 

Check the User Account Control 

Control Panel, click on User Accounts

Change User Account Control settings and set to lowest level.

Go to network share [\\\\server\-sage\\sage](file://///server-sage/sage)  and copy full Installers folder to C drive.

Then run command prompt as administrator; and follow the steps below. 

Type CD \\ and enter

Type CD Installers and enter

Type dir/p (should look like C:\\installers\>dir/p)

Then C:\\installers\>setup.exe (follow setup instructions tick sage 200 client)

Locate Service Packs folder. CD to service pack folder (or copy Latest Service Pack to C Drive to make it easier)

Then C:\\sp(version x).msp

Once installation is complete, delete installer folder from C:\\\> 

**Common errors while installing sage 200 client setup** 

Firewalls (should be set to minimum)

Net framework 3\.5 (update via control panel → program \& features → click on Turn windows features on or off and tick the mentioned program
