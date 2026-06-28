---
title: Debugging and Logging methods in the new .net Excelerator and IP frameworks
tags:
- Logs
- Development
description: This describes some methods to debug and log installations of V3 Enterprise.
  It is intended for developers and support. Below is pasted from an Email…
created: '2017-01-25'
modified: '2017-01-25'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Debugging%20and%20Logging%20methods%20in%20the%20new%20-net%20Excelerator%20and%20IP%20frameworks.aspx
---

**This describes some methods to debug and log installations of V3 Enterprise. It is intended for developers and support.**

Below is pasted from an Email Sean did in November 2013: 

Agam has written the Log Viewer, which is available from the Excelerator menu. We need to look into deploying it server side as well. This requires the log to be written to using the Codis.Logging.Support.LogLayout layout. Using the Log Viewer makes reading the log a lot easier. 

## Server Side

(including fat client programs) there is a choice: 

1. WCF Diagnostics: Can be viewed using svctraceviewer.exe (which we should look into distributing). Useful for identifying WCF service level errors and viewing SOAP messages
2. Debug Tracing: Print all debug.print message to a log. Not in a format that Log Viewer can use, but could probably could ([http://stackoverflow.com/questions/515381/how\-to\-log\-trace\-messages\-with\-log4net).](http://stackoverflow.com/questions/515381/how-to-log-trace-messages-with-log4net%29.) Useful for seeing Debug.print messages already embedded in the code.
3. Injecting instances of Codis.Logging ILog. If you add it as a dependency in an object that is wired by the container, it should get wired in. There is Logger object created in the sageconfig.xml in API.Framework and Codis.Framework. This method should at least be used for routine auditing type messages sent as INFO. Maybe for debug information as the output is more accessible than that produced by 2\).
4. API Call tracing using a LoggingAdvice and AOP. This technique can be used to log any call (entry and exit) to an object created by AOP (but I've only tested it with the API). The output can be formatted in a format that can be read with the Log Viewer. 5\.       Fiddler– use to capture WCF messages. Probably not needed as WCF Diagnostics can be used.

## Client side

1. Codis.Logging ILog. If you add it as a dependency in an object that is wired by the container, it should get wired in. You can turn on/off this logging from the Options in Excelerator, but if I understand correctly, you have to amend the app.config to choose the logging level.
2. Fiddler – use to capture WCF messages

### Server side configurations

Sample Configurations for 4\). A LoggingAdvice object should be defined and intercepted in the API AOP configuration. 

In Codis.WCF.SageEnterprise.CBReceipts – which is currently soft coded and deployed:



```xml
<object name="LoggingAdvice" type="Spring.Aspects.Logging.SimpleLoggingAdvice, Spring.Aop">
     <property name="LogUniqueIdentifier" value="true"/>
     <property name="LogExecutionTime"    value="true"/>
     <property name="LogMethodArguments"  value="true"/>
     <property name="LogReturnValue"      value="true"/>
     <property name="Separator"           value=";"/>
     <property name="LogLevel"            value="DEBUG"/>
     <property name="HideProxyTypeNames"  value="true"/>
     <property name="UseDynamicLogger"    value="true"/>
     <property name ="LoggerName" value ="CallTrace" />
   </object>
   <object id="CBReceiptsAPIServicesProxy" type="Spring.Aop.Framework.AutoProxy.ObjectNameAutoProxyCreator, Spring.Aop" singleton ="false">
     <property name="ObjectNames">
       <list>
         <value>CBReceiptsIPAPI</value>
         <value>CBPaymentsIPAPI</value>
       </list>
     </property>
     <property name="InterceptorNames">
       <list>
         <value>ApplyPermissionsIfAttribute</value>
         <value>LoggingAdvice</value>
       </list>
     </property>
   </object>
```

In the web.config:



```xml
<logger name="CallTrace">
       <level value="DEBUG"/>
       <appender-ref ref="CallTraceRollingLogFileAppender"/>
     </logger>
```

This appender does Log Viewer format:



```xml
<appender name="CallTraceRollingLogFileAppender" type="log4net.Appender.RollingFileAppender">
       <file value="c:\log\CallTrace.log"/>
       <appendToFile value="true"/>
       <maxSizeRollBackups value="10"/>
       <maximumFileSize value="5MB"/>
       <rollingStyle value="Size"/>
       <staticLogFileName value="true"/>
       <layout type="Codis.Logging.Support.LogLayout">
         <ItemsToInclude value="date,logger,,message,user,level,machinename,hostname,method,linenumber,thread,class"/>
       </layout>
     </appender>
```

Sample configuration for 1\) In web config:



```xml
<system.serviceModel>
   <diagnostics>
       <messageLogging
            logEntireMessage="true"
            logMalformedMessages="true"
            logMessagesAtServiceLevel="true"
            logMessagesAtTransportLevel="false"
            maxMessagesToLog="3000"
            maxSizeOfMessageToLog="65535000"/>
     </diagnostics> And
 <system.diagnostics>
   <sources>

       <source name="System.ServiceModel"
               switchValue="Information, ActivityTracing"
               propagateActivity="true" >
          <listeners>
             <add name="xml"/>
          </listeners>
       </source>
       <source name="System.ServiceModel.MessageLogging">
          <listeners>
             <add name="xml"/>
          </listeners>
       </source>
    </sources>
     <trace autoflush="true" />
    <sharedListeners>

       <add name="xml"
            type="System.Diagnostics.XmlWriterTraceListener"
            initializeData="C:\log\Traces.svclog" />
    </sharedListeners>
```

Sample Configuration for 2\)



```xml
<trace autoflush="true">
   <listeners>
     <add name="SyncListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="C:\log\"/>
   </listeners>
 </trace>
```

Sample Configuration for 3\) Below configures a logger for level Debug. Our logger can use this and other levels.



```xml
<log4net debug="false">
     <logger name="Debug">
       <level value="DEBUG"/>
       <appender-ref ref="DebugFileAppender2"/>
     </logger>
     <appender name="DebugFileAppender2" type="log4net.Appender.FileAppender">
       <file type="log4net.Util.PatternString" value="Debug.log"/>
       <lockingModel type="log4net.Appender.FileAppender+MinimalLock"/>
       <appendToFile value="true"/>
       <maxSizeRollBackups value="10"/>
       <maximumFileSize value="5MB"/>
       <rollingStyle value="Size"/>
       <staticLogFileName value="true"/>
       <!--<layout type="log4net.Layout.PatternLayout">-->
       <layout type="Codis.Logging.Support.LogLayout">
         <ItemsToInclude value="date,logger,,message,user,level,machinename,hostname,method,linenumber,thread,class"/>
       </layout>
     </appender>
```
