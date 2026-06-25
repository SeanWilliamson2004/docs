---
title: Configuring log4net logging
tags:
- Development
- Codis IP
description: Configuring Logging Configuration Location There is the option to define
  all the logging settings in the web/application configuration file for each…
created: '2019-10-16'
modified: '2019-10-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Configuring%20log4net%20logging.aspx
---

Configuring Logging

  
 

Configuration Location

There is the option to define all the logging settings in the web/application configuration file for each webservice or in an external file.  The latter allows you to have a single logging configuration for all webservices.

The factoryAdapter tag in the logging section defines where the logging configuration will be read from.  To read from the web/application configuration file enter:

  \<common\>

    \<logging\>

    \<factoryAdapter type\="Common.Logging.Log4Net.Log4NetLoggerFactoryAdapter, Common.Logging.Log4Net"\>

        \<arg key\="configType" value\="INLINE"/\>

      \</factoryAdapter\>

  
 

To read the configuration from another file enter:

  
 

     \<factoryAdapter type\="Common.Logging.Log4Net.Log4NetLoggerFactoryAdapter, Common.Logging.Log4Net"\>

        \<arg key\="configType" value\="FILE"/\>

        \<arg key\="configFile" value\="c:/Program Files/Codis Excelerator/LoggingConfig/log4net.config"/\>

      \</factoryAdapter\>

    \</logging\>

  \</common\>

  
 

Each webservice that uses the configuration file must have access to read the shared configuration file

  
 

Logging Configuration

  
 

To enable logging there must be an entry for the "Logger" and an entry for the "appender" used by the logger. 

  
 

Logger

The logger corresponds to an event being logged, and must be given the appropriate name for that event.

  
 

Soap Messages : "SoapMessage"

Security (logins, login attempts): "Security"

  
 

This is a typical logger definition

  
 

   \<logger name\="SoapMessage"\>

      \<level value\="OFF"/\>

      \<appender\-ref ref\="SoapMessageRollingLogFileAppender"/\>

    \</logger\>

  
 

The level determines what level of logging is activated.  The levels are:OFF, INFO, ERROR and DEBUG.  Which events this corresponds to depends on the logger.

  
 

The appender\-ref defines which appender is used.

  
 

Appender

The appender defines how the information is logged.  e.g. will it be a rolling file?  What is the file name?
