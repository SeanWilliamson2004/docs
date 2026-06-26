---
title: Creating Excelerator Plugins
tags:
- V3
- Consultancy
description: Menu Plugins There are two types of Excelerator menu plugins Those that
  appear in their own Excel ribbon menu item. Each plugin will have its own…
created: '2017-04-06'
modified: '2017-07-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Creating%20Excelerator%20Plugins.aspx
---

# Menu Plugins

There are two types of Excelerator menu plugins

- Those that appear in their own Excel ribbon menu item.  Each plugin will have its own button in the menu item.
- IExClientCustomGroup

 To create a menu plugin:

1. Create a new solution in Visual Studio.
2. Add a paket.references with the following lines. Install the packages.   
Codis.Sage200\.Base.Types  
Codis.Excelerator.Plugin.Types
3. Create a plugin class that implements Codis.Excelerator.Plugin.Types.IExClientPlugin.  Depending on the product you are developing for, you should choose one of the sub\-interfaces:
- **IExClientPluginS1000** for Sage 1000 Standard.
- **IExClientPluginS1000EE** for Sage 1000 Enterprise
- **IExClientPluginS200** for Sage 200

5. Implement the interface.
- The AssemblyTypes property determines which assemblies will be passed to the Run method.  If the plugin is not appearing in a group, the first assembly given in this list will be used to place the plugin in an existing menu.
- The Run method implements the functionality of the run in.  It will be passed instances of all the assemblies in the AssemblyTypes that implement the   
IExClientPluginApi interface. (This is done by Codis developers.)

To implement a group of plugins, you must:

1. Create a class that implements IExClientCustomGroup.
	1. Depending on the product you are developing for, you should choose one of the sub\-interfaces:
	2. **IExClientCustomGroupS1000** for Sage 1000 Standard.
	- **IExClientCustomGroupS1000EE** for Sage 1000 Enterprise
	- **IExClientCustomGroupS200** for Sage 200

Samples in Codis.Plugins.Test.vbproj in the CodisDevelopment repo.
