---
title: Residents Guestline Integration
tags:
- Support
- Orchestrator
description: Overview Codis have implemented an integration between Guestline (https://www.guestline.com/)
  and Sage 200 Cloud - which became Sage 200 On-Premis.…
created: '2022-03-11'
modified: '2024-02-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Residents%20Guestline%20Integration.aspx
---

## Overview

Codis have implemented an integration between Guestline (https://www.guestline.com/) and Sage 200 Cloud \- which became Sage 200 On\-Premis.  

Guestline is a hotel management system.  Revenue is recorded in this system, which has to be reflected in the Sage 200 accounts.  To do this, an Orchestrator instance on a server polls a Guestline web service daily to extract revenue and a Sage 200 journal is created.  

## Deployment

Sage 200 Cloud complicated this deployment considerably.    

We are limited as to the components we can deploy on the cloud server, and because of this, we cannot deploy web services as we did for the Mollies Apaleo Integration.aspx.   

There are additional components required to allow the connection to the cloud instance to be maintained.  

## Incoming Data

The webservice used https://pmsws.eu.guestline.net/rlxsoaprouter/rlxsoap.asmx,  rather than being a 'revenue' webservice like Apaleo, provides information according to a report template preconfigured in Guestline \<details on where\>.  As part of this configuration you can choose which revenue to report on.

The webservice then provides lines of revenue information as a product code, and net and a gross value.  The product code are mapped to Sage 200 NL codes using the Orchestrator mapping service.
