---
title: Excelerator Deployment Configurations
tags:
- Development
description: Overview Enterprise accounting software uses the client server model
  Client Server model. Sage 200 has a cloud server version available. See Sage 200…
created: '2017-03-01'
modified: '2017-03-02'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20Software%20Deployment%20Configurations.aspx
---

# Overview

Enterprise accounting software uses the client server model [Client Server model.](https://en.wikipedia.org/wiki/Client%e2%80%93server_model)  

Sage 200 has a cloud server version available.  See Sage 200 Product Range Overview.aspx

Codis' products, in particular Excelerator can be deployed in a number of different ways depending on the Sage product being used and the customer's requirements.  Our software components can be deployed to:

1. Client side.  This is usually the user's PC.  However, in some configurations users (Citrix or Terminal Services) don't run software on their PC, but run from a central server that supplies software to their PC.  In these configurations, client side components are installed usually installed on the Citrix or Terminal Services server.
2. Server side. This is on a central server often but not always on the customer's site.
3. Cloud side.  This is also on a central server but one on the cloud that is hosted by a 3rd party.  In some configurations, servers as described in (2\) can be hosted on the cloud.

# Codis Product Configurations

## Sage 1000

Codis software can be deployed in the following configuration:

- Standard Excelerator \- all components are installed on the client and the software communicates directly with the Sage 1000 databases.
- Web services \- components are installed server side for third party software to communicate with.
- Enterprise Excelerator \- as for web services, except Excelerator client software is installed client side.

[http://www.codis.co.uk/IntegrationPlatformHelp/](http://www.codis.co.uk/IntegrationPlatformHelp/)

## Sage 200

Codis software can be deployed in the following configuration:

- Standard Excelerator \- all components are installed on the client and the software communicates directly with Sage 200 server components including the database via Sage 200 APIs.
- Web services \- components are installed server side for third party software to communicate with.  This solution cannot be deployed to a Sage Extra cloud server directly.
- Cloud Excelerator \- some components are installed client side and some components are deployed to the Sage 200 Cloud server.
