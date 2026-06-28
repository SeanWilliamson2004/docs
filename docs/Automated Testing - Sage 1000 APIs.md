---
title: Automated Testing - Sage 1000 APIs
tags:
- Testing
description: This page describes the techniques used for automating tests of Codis
  software that works with Sage 1000. It is aimed at developers. There is also a…
created: '2017-01-23'
modified: '2017-01-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Automated%20Testing%20-%20Sage%201000%20APIs.aspx
---

**This page describes the techniques used for automating tests of Codis software that works with Sage 1000\. It is aimed at developers. There is also a link to a list of tests and the results.** 

## Test classes

Generally, test classes should inherit from Codis.SageEnterprise.Test.TestBase or Codis.SageEnterprise.Test.RollbackTestBase. These classes themselves inherit from [AbstractDependencyInjectionSpringContextTests](http://www.springframework.net/doc-latest/reference/html/testing.html) and [AbstractTransactionalSpringContextTests](http://www.springframework.net/doc-latest/reference/html/testing.html) respectively. Both of these classes provide a convenient way of injecting dependencies, and the latter encapsulates tests in a transaction that is rolled back at the end of the test. See [http://www.springframework.net/doc\-latest/reference/html/testing.html](http://www.springframework.net/doc-latest/reference/html/testing.html) They also include TestInitialisation methods that will set the Sage database configuration object in the [container](Codis Development Framework - IOC Spring.Net.md).

## System Keys and Project Settings

System keys and Project Settings control different configurations of Sage 1000\. We need to test that our APIs behave correctly under these differing configurations. It would be difficult to have lots of different datasets, each with a different system key combination and project settings, so to work around this, we have a means of overriding this settings for individual tests. As we use [IOC Principles](http://www.springframework.net/doc/reference/html/background.html#background-ioc) and the [Spring IOC Container](http://www.springframework.net/doc-latest/reference/html/objects.html), why can replace the object used to retrieve Sage configuration. This is done in the Codis.SageEnterprise.Test ObjectConfiguration.xml file with the lines: 



```xml
<object name="SageConfig" type="Codis.SageEnterprise.Test.TestConfiguration, Codis.SageEnterprise.Test" />
<object name="ProjectConfig" type="Codis.SageEnterprise.Test.TestProjectConfiguration, Codis.SageEnterprise.Test" />
```

Providing this file is included in your container configuration after the standard configurations for these objects in Codis.SageEnterprise.Common, the Test objects will be used. 

Project settings can then be set in a test: 



```vbnet
ProjectConfig.UseDa0659 = True
```

and system keys overridden: 



```vbnet
SageConfig.OverrideKey("NLYEAR", "14")
```

## Setting the Target Sage Database

**Tests should use only [supported test databases or their deltas](Baseline Testing.md).**  These databases are controlled with versioned backups kept. In some cases tests have been developed that use test databases that are no longer supported. Ideally, these should be changed to use supported databases, but sometimes this may be too time consuming. If inheriting from TestBase or RollbackTestbase, the database connection string is taken from the overrideable readonly property TargetDBConnectionString which by default uses the TargetDbServer and TargetDatabase overrideable properties to build the connection string. Using the app.config to determine the connection string is now obsolete. 

### TargetDatabase

Override this property to set the Target sage test database used by all tests in the class. 

### TargetDBServer

This reads the environment variable TARGETSERVER. If this is not found, "(local)" is used. This will allow us to override the target server for test runs. ## Checking which database you are using

You can check which target Sage database is being used with the following code. You do not have to use CECurrencyDAO. Any DAO will do.



```vbnet
Public Property CECurrencyDAO() As ICECurrencyDAO
<TestMethod> _
Public Sub ValidateTest()
    Debug.Print("Connection string:" & CType(CType(CECurrencyDAO, AdvisedProxy).m_targetSource.GetTarget, CECurrencyDAO).DbProvider.ConnectionString)
End Sub
```


## Mocks Classes

Mock classes can be used to create a particular set of conditions for a test. You can mock DAO classes to mock data conditions. When using Spring tests that have public properties that are wired and persist for all tests in a class, if you reassign any property of those instances to a mock instance then that reassignment may persist into other tests. Use SetDirty at the end of the test to force a rewire.   
## Results

Details of the current Sage 1000 tests and their results can be found here: [\\\\cd01sr16104\\Testing\\CodisWikiDev\\S1000TestResults.xlsx](file://///cd01sr16104/Testing/CodisWikiDev/S1000TestResults.xlsx)
