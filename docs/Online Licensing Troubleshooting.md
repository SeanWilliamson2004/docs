---
title: Online Licensing Troubleshooting
tags:
- Support
- Licensing
description: 'Troubleshooting client''s errors See also: Excelerator Client Installation
  and Setup Guide.aspx This diagnostic tool: DiagnosticWithUI can be used to…'
created: '2020-01-15'
modified: '2023-11-29'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Online%20Licensing%20Troubleshooting.aspx
---

## Troubleshooting client's errors

See also: [Excelerator Client Installation and Setup Guide.aspx](Excelerator Installation Troubleshooting.md)

This diagnostic tool:  [DiagnosticWithUI](/:u:/s/Wiki/EbE6LKbC7DBKmJD4kLMskkwBMWsUBChf-6a1EGRdmGzhlQ?e=jJqVEH)can be used to diagnose errors with registering new PCs or with existing licences. Extract the folder and run a command line (in the folder shift \+ right click \+ "open powershell here"). From there type "lic" and TAB, it should auto complete to ".\\LicenceDiagnostic.exe". Follow one of the commands to use, eg ".\\LicenceDiagnostic.exe diag" or ".\\LicenceDiagnostic.exe read".  

## Firewall Ports \& URLs To Unblock

**TCP/IP Ports**  
Http: 80  
Https: 443  

**URLs**  
[https://auth.codis.co.uk](https://auth.codis.co.uk/) [https://licence.codis.co.uk](https://licence.codis.co.uk/)   
[https://my.codis.co.uk](https://my.codis.co.uk/)    
[https://login.microsoftonline.com](https://login.microsoftonline.com/)   
[https://accounts.google.com](https://accounts.google.com/)   
[https://accounts.google.co.uk](https://accounts.google.co.uk/)   
[https://login.live.com](https://login.live.com/)   
[https://secure.aadcdn.microsoftonline\-p.com](https://secure.aadcdn.microsoftonline-p.com/)   
[https://urs.microsoft.com](https://urs.microsoft.com/)   
[https://iecvlist.microsoft.com](https://iecvlist.microsoft.com/)   
[https://auth.gfx.ms](https://auth.gfx.ms/)

## Common Issues

Registration Screen Flashes past without a chance to enter your Microsoft or Google ID.  

This happens because there is already a Microsoft or GoogleID is already held in a cookie.  You can remove all cookies or change the default browser but it is probably easier to copy the path that is displayed for the web page asking to choose which provider, and to paste that into an In\-Private windows (for IE) or a Incognito window (for Chrome).  

\- If the licence keeps changing Licence Method

check the registry with the below location where licence method is stored.

It would be goo d to check HKLM\\Software\\Codis\\Excel

This might change with Windows/Office updates.

We need to change the method in registry to the one we licenced the product for.
