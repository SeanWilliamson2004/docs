---
title: Missing Excelerator tab "Registering adxloader.dll"
tags:
- Solution
description: Before you apply solution below please close all Excel. Please see step
  by step instruction below to resolve missing Excelerator tab. 1. Log in to…
created: '2017-03-27'
modified: '2017-03-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Missing%20Excelerator%20tab%20Registering%20adxloader-dll.aspx
---

Before you apply solution below please close all Excel.

 Please see step by step instruction below to resolve missing Excelerator tab. 

1\.       Log in to the pc as user and run command prompt as Administrator (see below)

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar1.jpg) 

2\.       CD\\ and Enter

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar2.jpg) 

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar3.jpg) 

3\.       Unregister adxloader.dll to do so type in (regsvr32 –u adxloader.dll) and press Enter (see below)

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar4.jpg) 

4\.       Register adxloader.dll (type in regsvr32 adxloader.dll) and press Enter (See below)

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar5.jpg) 

5\.       Once its successfully registered, open excel as normal and see if Excelerator tab is displayed, if not. Follow instruction below. 

6\.       In Excel, click on File and select Options.

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar6.jpg) 

7\.       Select Add\-Ins and from Manage drop down list select COM Add\-Ins and Click Go (see below)

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar7.jpg) 

8\.       If Codis Excelerator option is not ticked in box below, tick it and select OK.

![](images/Support_Support_Wiki_Images_Images_for_solutions_toolbar8.jpg) 

Also click on link to our webpage help below on how to resolve missing Excelerator ribbon issue;

[http://www.codis.co.uk/excelerator\-help/quick\-installation\-instructions/common\-installation\-issues/issue\-1\-\-\-excelerator\-ribbon\-not\-present](http://www.codis.co.uk/excelerator-help/quick-installation-instructions/common-installation-issues/issue-1---excelerator-ribbon-not-present)
