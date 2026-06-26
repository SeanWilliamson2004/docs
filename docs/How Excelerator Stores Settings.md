---
title: How Excelerator Stores Settings
tags:
- Excelerator
description: Excelerator stores configuration settings in a number of locations and
  uses different mechanisms to save them. The choice of location or mechanism…
created: '2018-10-11'
modified: '2018-10-11'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/How%20Excelerator%20Stores%20Settings.aspx
---

Excelerator stores configuration settings in a number of locations and uses different mechanisms to save them.

The choice of location or mechanism might be because of the scope of the setting (user, machine).  In some cases, the decision might have been made before issues with multi\-user environments (e.g. Citrix) became more prevalent, but have been kept to avoid the impact that losing settings should an existing site be upgraded.  

# Roaming and Local Profile Locations

Most configuration files are stored in these locations that are based on the user.

Local Profile location: {SpecialFolder.LocalApplicationData}\\Codis\\Excelerator

Roaming Profile location: {SpecialFolder.ApplicationData}\\Codis\\Excelerator.

{SpecialFolder.ApplicationData} and {SpecialFolder.LocalApplicationData} can vary by operating system.  See [Wikipedia Special Folders page.](https://en.wikipedia.org/wiki/Special_folder)

Be aware that in sites that use roaming profiles for their users, it is common practice to redirect the roaming profile folder to point at a shared network location.  


# ConfigurationManager Files

Some settings are stored in roaming or local profile configuration files using the Microsoft Configuration API.   

As of release xxxx the software will switch storing in the roaming profile to the local profile when an error is encountered saving or getting the roaming configuration.    


# General Settings

These are:

- [Designer Advanced Tools options](http://www.codis.co.uk/excelerator-help/customise-excelerator/designer-advanced---tools-options)
- Screen Layout and log settings
- Spreadsheet input output

These are stored in the roaming profile application manager file User.config.

# V3 Sage 1000 Standard Connection Settings

These are stored in the local profile application manager file User.config.  They really should be stored in the roaming profile.

# Per Module Options

Stored in the roaming profile location application manager file UserOptions.config.

# V3 Sage 1000 Enterprise Endpoints

Stored in the roaming profile location application manager file UserOptions.config
