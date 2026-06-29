---
title: Sage 200 Hypers - developers
tags: []
description: Development machines usually want to have a Sage client running on their
  PC that can connect to a Sage server instance on a hyper. Sometimes, there…
created: '2024-09-23'
modified: '2024-09-24'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Hypers%20-%20Developers.aspx
---

Development machines usually want to have a Sage client running on their PC that can connect to a Sage server instance on a hyper.  Sometimes, there can be particular challenges in getting this configuration to work.  

Below are some troubleshooting notes:  

A good first step is to configure the firewalls on both machines.

# Firewall Configuration

Rather than turn off more firewall protection is needed, the best approach is to ensure that the hyper is a "Private" computer, and that "Private" connections are not checked on either the PC or the hyper.  

I think that turning on network discovery on the hyper will ensure is is a "Private" computer.  Network and Sharing Centre\-\>Change Advanced Sharing Settings:

![2024-09-23_13-27-02.png](images/PublishingImages_Pages_Sage_200_Hypers_-_developers_2024-09-23_13-27-02.png)  

Then, Windows Defender with Advanced Firewall Settings\-\>Windows Defender Firewall Properties.  "Public" and "Domain" profiles firewall state should be on.  "Private" profile should be Off.  

# Errors

## Communication Error: There was no endpoint listening at..

![2024-09-23_13-13-36.png](images/PublishingImages_Pages_Sage_200_Hypers_-_developers_2024-09-23_13-13-36.png)  

This error could have several causes, sometimes in combination.  First of all, the client must use the correct IP address to connect to the server.  The IP address is usually defined in the hosts file.    

The Sage client will use the server name in its configuration file (need to find the name of this), and the name it is using can be seen in the connection failure message.  

Note: As of writing, the Sage200C2024R1 hyper server instance is named Sage200C2023R2\.  Renaming it will break Sage, which has the server name in some configurations.  It is probably best to use the same name in the hosts and client configuration.  

If you are confident that you are trying to connect to the correct IP address but the connection still fails with this same message, it could be due to the firewall.  

## Communication Error: Could not establish trust relationship...

![2024-09-19_12-26-00.png](images/PublishingImages_Pages_Sage_200_Hypers_-_developers_2024-09-19_12-26-00.png)  

I think this was solved by adding the correct certificate from the Logon folder.  The certificate is associated with the server name.  

[Sage 200 Professional \- "The remote certificate is invalid" or ""Could not establish trust relationship"error](https://gb-kb.sage.com/portal/app/portlets/results/viewsolution.jsp?solutionid=200427112311684)  

## Communication Error: The HTTP request is unauthorized with client authentication scheme 'Negotiate'

![2024-09-24_08-22-10.png](images/PublishingImages_Pages_Sage_200_Hypers_-_developers_2024-09-24_08-22-10.png)  

https://communityhub.sage.com/gb/sage\-200/f/general\-discussion/201281/communication\-error  

I resolved this by adding the user Administrator in the Windows credentials for the server name being accessed:  

![2024-09-23_11-48-24.png](images/PublishingImages_Pages_Sage_200_Hypers_-_developers_2024-09-23_11-48-24.png)
