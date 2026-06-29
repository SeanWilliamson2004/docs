---
title: Excelerator Installation - adxloader
tags:
- Excelerator
- Development
- Support
- Installation
description: Add-in Express™ How Office COM add-ins are registered and loaded As it
  is frequently stated throughout this manual, an Office solution must be…
created: '2017-01-26'
modified: '2020-03-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Installation%20-%20adxloader.aspx
---

## [Add\-in Express™](https://www.add-in-express.com/docs/net-deploying-addins.php)

## How Office COM add\-ins are registered and loaded

As it is frequently stated throughout this manual, an Office solution must be registered so that the corresponding Office application (Outlook, Excel, Word, PowerPoint etc.) is able to locate and load it. Add\-in Express creates registry keys itself but because some keys are created in HKEY\_CURRENT\_USER (HKCU) and some in HKEY\_LOCAL\_MACHINE (HKLM), the user running the installer must have permissions for the corresponding registry hive. So, you should always consider the permissions or privileges when choosing the way to deploy your Office addin.

**See related videos:**

- [Fully featured setup projects for Office solutions](https://www.add-in-express.com/creating-addins-blog/2011/05/26/deployment-fully-featured-setup-video/)
- [Add\-in Express deployment models \- ClickOnce and ClickTwice :)](https://www.add-in-express.com/creating-addins-blog/2010/11/12/office-deployment-clickonce-clicktwice-video/)

Further on this page you will find the detailed information about:

- [How your Office add\-in is registered](https://www.add-in-express.com/docs/net-deploying-addins.php#extension-registered)
- [How your Office extension loads into an Office application](https://www.add-in-express.com/docs/net-deploying-addins.php#load)
- [Add\-in Express loader](https://www.add-in-express.com/docs/net-deploying-addins.php#loader)
- [Add\-in Express loader manifest](https://www.add-in-express.com/docs/net-deploying-addins.php#loader-manifest)

## How your Office add\-in is registered

A setup project created as described in [Creating MSI Installers](https://www.add-in-express.com/docs/net-msi-setup-project.php) uses adxregistrator.exe as a custom action. When you run the installer and adxregistrator.exe is invoked, it performs the following steps:

- loads .NET Framework
- creates an instance of the add\-in module
- invokes the registration code provided by the Add\-in Express module; there is a special module for each Office extension type, see [Add\-in Express modules](https://www.add-in-express.com/docs/net-components-overview.php#adx-modules)

When doing all the things above, adxregistrator.exe writes them into a log file, its default location is `{user profile}`\\Documents\\Add\-in Express\\adxregistrator.log. What follows below is a description of the process and how you can customize it. See also [Troubleshooting add\-in registration](https://www.add-in-express.com/docs/troubleshooting-tips.php#troubleshooting_add-in_registration) and [Shims, Loader and Add\-in Express .NET Setup projects](https://www.add-in-express.com/creating-addins-blog/2006/08/04/shim-loader-mscoree/) and the Addin Express developers guide: [adxnet.pdf](https://codislimited.sharepoint.com/sites/Wiki/Development/adxnet.pdf)

### Specifying the assembly to register

adxregistrator.exe supports /install and /uninstall switches. They accept a string parameter containing the file name of the assembly that is to be registered/unregistered.

adxregistrator.exe /install\="MyAddin1\.dll"

All addin files including dependencies and the Add\-in Express assemblies must be located in the folder where adxregistrator.exe is run.

### Registration\-time privileges

An Office COM add\-in has two sides: it is a COM class and an Office addin at the same time. Both sides of the COM add\-in require proper registration in the Windows Registry.

The **add\-in** side of a COM add\-in relates only to Office: a per\-user COM addin is denoted by False in the RegisterForAllUsers property of its add\-in module and it is registered in HKCU. A per\-machine plug\-in has True in the RegisterForAllUsers property of its add\-in module and it is filed down in HKLM. The exact registry paths are given in [Registry keys](https://www.add-in-express.com/docs/net-deploying-addins.php#registry-keys).

Before you modify the RegisterForAllUsers property, you must unregister the add\-in project on your development PC and make sure that adxloader.dll.manifest is writable.

But the **COM class** side of a COM add\-in, the COM object implemented by the add\-in module and corresponding to the add\-in as a whole, must be registered, too. It can be registered either in HKCU or in HKLM (the same as the add\-in side). This is controlled by the /privileges switch supported by adxregistrator.exe. The switch accepts two values: admin and user. Misspelling the value or omitting the switch results in registering the COM object of the Office COM add\-in in HKLM and this requires administrative permissions.

The need to register both, the COM class and the Office add\-in itself, creates four possible combinations of settings you can specify in RegisterForAllUsers and in the /privileges switch of adxregistrator.exe. The two combinations below are recommended:

- per\-user add\-ins:  
add\-in module: RegisterForAllUsers \= False  
adxregistrator.exe: /privileges\=user
- per\-machine add\-ins:  
add\-in module: RegisterForAllUsers \= True  
adxregistrator.exe: /privileges\=admin

Please note that for a per\-machine extension, all users must have appropriate permissions for the folder the plugin is installed to. The Add\-in Express team recommends installing such an add\-in to Program Files.

### CLR version to use while registering

By default, adxregistrator.exe loads the latest version of the .NET Framework installed on the PC. This can be a problem if your assembly uses version\-sensitive components. To bypass this, you can use the /CLRVersion switch that accepts a string value in the format below:

| major\[\[.minor].build] |
| --- |

The value you assign to a switch is processed as described below:

- \\CLRVersion\="2\.0\.50727" refers to the specified build of the .NET Framework. If the build with the exact build number is not installed on the PC, the newest of all .NET Framework versions installed on the PC will be loaded. This will also occur if any other build of .NET Framework 2\.0 is installed on the PC.
- \\CLRVersion\="2\.0" refers to any build of .NET Framework 2\.0\. In a hypothetical scenario with the now non\-existing .NET Framework 2\.1 installed, using \\CLRVersion\="2\.0" will result in loading the latest version of the .NET Framework installed on the PC (after the registrator does not find .NET Framework 2\.0\).
- \\CLRVersion\="2" refers to any build of .NET Framework 2\.0\.

If the specified version of the .NET Framework is not installed on the PC, the newest version of all .NET Framework versions installed on the PC is loaded instead.

### Creating an instance of the add\-in module

After the CLR is loaded, the registrator creates an AppDomain, loads the assembly specified by you (see [Loading the assembly](https://www.add-in-express.com/docs/net-deploying-addins.php#loading-assembly)), creates an instance of the Add\-in Express module defined in the assembly and run the registration code provided by every module of Add\-in Express. If the assembly includes several Add\-in Express modules (\=several Office add\-ins), the registrator processes all of them in turn.

### Registering. An important note

Creating an instance of the module invokes the module's constructor. It means that you should foresee the situation in which the module is created outside of the Office application. If you don't, a run\-time exception may prevent your Office plugin from being registered or unregistered. The simplest way to bypass this is not to write custom code in the constructor of the module. Instead, you can use the events the module provides.

**Note.** Do not write custom code in the constructor of the module.

If a variable in the module is declared on the class level, the initializer of the variable is called even before the constructor of the module. That is why all the reasoning for not using custom code in the module's constructor does apply to initializers.

**Note.** Do not use initializers of complex\-type variables declared on the class level in the module.

### Running the registration code

Every Add\-in Express module provides a static (Shared in VB.NET) method with the ComRegisterFunction attribute applied. That method invokes the registration code defined in the base class of the module. Note that if you create a custom static (Shared in VB.NET) method and apply ComRegisterFunction to it, the method will be executed during registration. The ComUnregisterFunction attribute is processed in a similar fashion; if this attribute is applied to a method, the method will be called while unregistering the extension. There's no way to predict or change the order in which methods having such attributes are called.

### Get details about add\-in registration/unregistration

The process of registration/unregistration is documented in a log file, the default location of which is `{user profile}`\\Documents\\Add\-in Express\\adxregistrator.log. The registrator supports the /LogFileLocation switch that allows you to specify the path and file name of the log file. Also, the log file will not be generated if you use /GenerateLogFile\=false; omitting that switch means the file will be generated.

When specifying the path to the log file, you can refer to a system folder using a widespread notation, a sample of which is %UserProfileFolder%. Below is the list of supported folder IDs (please find their definitions here ):

- ProgramFilesX64Folder
- RoamingAppDataFolder
- DesktopFolder
- PersonalFolder
- InternetCacheFolder
- LocalAppDataFolder
- AppDataFolder
- DocumentsFolder
- MyDocumentsFolder
- UserProfileFolder
- ProgramFilesFolder
- CommonProgramDataFolder
- PublicDocumentsFolder
- PublicDesktopFolder
- ProgramFilesX64CommonFolder
- ProgramFilesCommonFolder

The supported macro characters are as follows: \<\>, \&\&, \[], $$, %%.

### Exit code

If a custom action returns a non\-zero exit code, the .MSI installer produces nasty dialogs that may scare the end user and produce extra problems for the developer. That is why, the default value of the /ReturnExitCode switch supported by the registrator is false. Nevertheless, in custom scenarios you may want to be notified about problems as soon as possible. Set the switch to true and get a value that you can decipher using the information supplied here.

## How your Office extension loads into an Office application

When a user starts an Office application, the application locates the Add\-in Express loader, which is an unmanaged DLL that loads the add\-in assembly. The following figure shows the basic architecture of Add\-in Express based add\-ins. 

![The basic architecture of Add-in Express based add-ins](images/https_www.add-in-express.com_images_net-docs_2013_office-addin-architecture.png)### Loading process

The following steps occur when a user starts an Office application.

1. The application locates the registry entries that identify your Office add\-in. These records are created as part of the registration process.
2. If the application finds the corresponding registry entries, it loads either adxloader.dll (32bit Office applications) or adxloader64\.dll (64bit Office). The installer of your add\-in deploys these DLLs to the add\-in's installation folder.
3. The loader reads the manifest, which is located in the same folder and locates the add\-in assembly. If the manifest specifies this, a log file is created at the specified location. See also [Add\-in Express loader manifest](https://www.add-in-express.com/docs/net-deploying-addins.php#loader-manifest) and [Get details about add\-in loading](https://www.add-in-express.com/docs/net-deploying-addins.php#log).
4. The loader initializes CLR, creates an AppDomain using the configuration file specified by the manifest, loads your assembly into the domain, and creates an instance of your add\-in module.
5. When one of the start\-up events is received on the IDTExtensibility2 and IRibbonExtensibility COM interfaces, the loader translates the call to the AddinInitialize and OnRibbonBforeCreate events of the add\-in module, respectively, and in this way your assembly starts functioning as an Office add\-in.

### Registry keys

Any Office solution \- a COM add\-in, Excel add\-in, RTD server, or smart tag \- must be installed and registered because Office looks for extensions in the registry. In other words, to get your extension to work, 1\) add\-in files must be installed to a location accessible by the add\-in users and 2\) registry keys must be created that specify which Office application will load the plug\-in and which PC users may use the add\-in. The necessity to create registry keys is the reason why **you cannot use XCOPY deployment** for an Office COM add\-in, Excel XLL, RTD server, or Smart tag. 

Although Add\-in Express creates all registry keys for you, you might need to find the keys when debugging your add\-ons. The main intention of this section is to provide you with information on this.

#### Locating COM add\-ins in the registry

We use these terms to name the registry keys described below:

- add\-in key
- ProgId key
- CLSID key

Depending on the value of the RegisterForAllUsers property of the add\-in module (to access it in the Properties window, click the designer surface of the module), the main registry entry of a COM add\-in, the add\-in key is:

| `{HKLM or HKCU}\Software\Microsoft\Office\{host}\AddIns\{your add-in ProgID}` |
| --- |

If the RegisterForAllUsers property of the add\-in module is true, the plug\-in is registered in HKEY\_LOCAL\_MACHINE, otherwise the key is located in HKEY\_CURRENT\_USER.

Pay attention to the *LoadBehavior* value defined in this key; typically, it is *3*. If *LoadBehavior* is *2* when your run your plug\-in, this may be an indication of an unhandled exception at add\-in startup.

The other keys – the ProgId key and CLSID key – are demonstrated in the figure below:

![Registry entries used by Office applications to locate and load a COM add-in](images/https_www.add-in-express.com_images_net-docs_2012_deployment_register-addin.png)#### Locating Excel UDF add\-ins in the registry

Registering a UDF adds a value to the following key:

| `HKEY_CURRENT_USER\Software\Microsoft\Office\{Office version}.0\Excel\Options` |
| --- |

The value name is OPEN or `OPEN{n}` where n is 1, if another UDF is registered, 2 \- if there are two other XLLs registered, etc. The value contains a string, which is constructed in the following way:

| str \= "/R " \+ "" \+ pathToTheDll \+ "" |
| --- |

If an Excel add\-in is turned off in the Excel Add\-ins dialog, see the path to the add\-in's loader in:

| `HKEY_CURRENT_USER\Software\Microsoft\Office\{version}.0\Excel\Add-in Manager` |
| --- |

## 

## Add\-in Express Loader

All Office applications are unmanaged while all Add\-in Express based plug\-ins are managed class libraries. Therefore, there must be some software located between Office applications and your add\-ins. Otherwise, Office applications will not know of your .NET add\-ins and other Office extensions. That software is called a shim. Shims are unmanaged DLLs that isolate your plugins in a separate application domain.

When you install your add\-in, the registry settings for the add\-in will point to the shim. And the shim will be the first DLL examined by the host application when it starts loading your add\-in or smart tag.

Add\-in Express provides the shim of its own, called Add\-in Express loader. The loader (adxloader.dll, adxloader64\.dll) is a compiled shim not bound to any certain Add\-in Express project. Instead, the loader uses the adxloader.dll.manifest file containing a list of .NET assemblies that must be registered. The loader's files (adxloader.dll, adxloader64\.dll and adxloader.dll.manifest) must always be located in the Loader subdirectory of the Add\-in Express project folder. When a project is being rebuilt or registered, the loader files are copied to the project's output directory. You can sign the loader with a digital signature and, in this way, create trusted extensions for Office.

### Add\-in Express loader manifest

The manifest (*adxloader.dll.manifest*) is the source of configuration information for the loader. Below, you see the content of a sample manifest file.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <assemblyIdentity name="MyAddin14, PublicKeyToken=f9f39773da5c568a" />
  <loaderSettings generateLogFile="true" shadowCopyEnabled="false"
                  privileges="user" configFileName="app.config"
                  minOfficeVersionSupported="{major[.minor]]}"
                  clrVersion="{major[[.minor].build]}">
  <logFileLocation>C:\MyLog.txt</logFileLocation>
 </loaderSettings>
</configuration>
```

The manifest file allows generating the log file containing useful information about errors on the add\-in loading stage. The default location of the log file is *`{user profile}`\\Documents\\Add\-in Express\\adxloader.log*. You can change the location using the *logFileLocation* attribute; relative paths and folder constants are acceptable, see [Get details about add\-in registration/unregistration](https://www.add-in-express.com/docs/net-deploying-addins.php#documenting-process). The manifest file allows you to enable the Shadow Copy feature of the Add\-in Express loader, which is disabled by default (see [Deploying \- shadow copy](https://www.add-in-express.com/docs/net-deploying-debugging-tips.php#Shadow%20copy)).

The *privileges* attribute accepts the *"user"* string value indicating that the Add\-in Express based setup projects can be run with non\-administrator privileges. Any other value will require administrator privileges to install your project. You should be aware that the value of this attribute is controlled by the *RegisterForAllUsers* property value of add\-in and RTD modules (to access it in the Properties window click the designer surface of the add\-in module or RTD server module). If *RegisterForAllUsers* is *True* and *privileges\="user"*, a standard user running the installer will be unable to install your Office extension. If *RegisterForAllUsers* is *False* and *privileges\="administrator"*, your Office extension will be installed for the administrator only.

Before you modify the RegisterForAllUsers property, you must unregister the add\-in project on your development PC and make sure that adxloader.dll.manifest is writable.

Use the *minOfficeVersionsupported* attribute to let the add\-in load in supported Office versions only. Omitting this attribute means that your add\-in will be loaded in any Office version from 2000 to the latest. Loading the add\-in using other conditions is discussed in [How to load your Office COM add\-in on condition](https://www.add-in-express.com/creating-addins-blog/2012/01/20/load-office-addin-on-condition/).

For more information about setting *clrVersion*, see [CLR version to use while registering](https://www.add-in-express.com/docs/net-deploying-addins.php#clr-version). The use of the *configFileName* attribute is described in [Configuring an add\-in](https://www.add-in-express.com/docs/net-office-tips.php#configuring-add-in).

Note that you can run *regsvr32* against the *adxloader.dll*. If a correct manifest file is located in the same folder, this will register all Add\-in Express projects listed in the loader manifest.

### Get details about add\-in loading

If the manifest requires creating a log file (see the *generateLogFile* attribute at [Add\-in Express loader manifest](https://www.add-in-express.com/docs/net-deploying-addins.php#loader-manifest)), the log file is created in the location specified by the manifest or in {Documents}\\Add\-in Express\\adxloader.log (default). The file is rewritten when when the Office application loads your add\-in.
