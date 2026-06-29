---
title: Development Operations Resilience
tags: []
description: Background Overview Codis Development Operations (DevOps) are the processes
  and enabling infrastructures that allow developers to bring ideas to…
created: '2018-11-22'
modified: '2018-12-04'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Development%20Operations%20Resilience.aspx
---

# Background

## Overview

## 

## 

Codis Development Operations (DevOps) are the processes and enabling infrastructures that allow developers to bring ideas to released software.  As part of a general effort to make Codis' operations more resilient by placing services on the cloud, this project discusses actions needed to move DevOps resources and operations to cloud based infrastructures.

There are fundamental differences between categories of cloud services available.  The different categories can be stacked starting with onsite hosted (not cloud), through IAAS, PAAS to SAAS ([WHAT’S THE DIFFERENCE BETWEEN SAAS, PAAS, IAAS?)](https://www.computenext.com/blog/when-to-use-saas-paas-and-iaas/), with onsite generally being the riskiest through to SAAS being the least.

Codis DevOps can be divided into two distinct streams.  Legacy operations that predated a move to .net, and .net operations.  The legacy operations were mostly superceeded by the .net operations but some do still exist.

## Non\-legacy Operations (Azure DevOps)

These are V3 .net programs.   .Net operations are controlled by Azure DevOps (formally TFS then VSTS).  Azure DevOps is a complete DevOps offering that integrates with task management and source control and automates builds and distribution of software.  The configuration side of Codis' Azure DevOps already resides on the cloud but build resources remain onsite.

Build and distribution services are carried out by two areas in Azure DevOps \- Builds and Release Management.   Both assign Build or Release pipelines to be built by pools of agents.  Agents can be hosted (by a SAAS provider, usually Microsoft) or self\-hosted on servers administered by Codis.  Self\-hosted agents have 'capabilities' e.g. the capability to run installshield, and pipelines have demands e.g. to demand the capability to run Installshield.

Non\-legacy builds and releases were designed before VSTS was available and with the intention of allowing multiple agents to run on different servers, but always delegating the Installshield tasks to the Development server (via a remote powershell process), and accessing shared folder resources.  These processes have various dependencies \- resources that have to be available to the build process. Currently these include:

- The build phase of S200 and S1000 Excelerator requires a Component One licence to be activated on the build server.
- The release phase requires an Installshield build engine.
- Sage 1000 Tests.
- Sage 200 test systems.
- Codis internal network file resources:
- Installer definitions
- Powershell scripts
- SQL Scripts
- Shares that are targets for the distribution of the packaged software.
- Referenced Assemblies

Many of these resources are not version controlled which in itself is not satisfactory.

## Legacy Operations

Legacy operations automate builds and some distribution of legacy software.  Generally, this software is VB6\.  All elements are based onsite with centralised resources on the "Development" server.   Builds are automated using Visual Build Pro.   Builds are made using the resources:

1. VSS database holding the code.  V1\.Net code is also in a Azure Repos Repo.  This conflict needs to be resolved.
2. Codis internal network including:
1. Installers (C:\\Development\\VB\\Installer, C:\\Development\\VB.NET\\Installer).  Not held in VSS.
2. Various other files including referenced dlls, sql scripts, most seemingly in the supporting files folder.
3. Distribution targets.  These are local folders that are shared.

## Installshield

Installshield is used by Legacy and Non\-Legacy software to package software.  There is probably 30 to 50 definitions, meaning that a wholesale move would be difficult.   Not so many of those definitions are used by non\-Legacy solutions \- appoximately 10\.  All solutions that migrate would require retesting.  

We have a single licence.  This allows maintenance of definitions and a non\-inactive builds to be run.  There should also be a standalone build engine available that can be installed on one other server.

## Component One

Component One components are used in Legacy and Non\-Legacy software.  A check is made at build time as to whether the software is licenced.   As such, all projects that use these components can only be built on a server where a licence is installed.

## Automated Tests

Codis' DevOps uses gateway tests that run as part of the build process to help ensure the quality of the software.

Core tests do not require any other components.  

Sage 1000 tests require access to a set of predefined databases.  These databases are defined as repo backups.  

Sage 200 tests are not current run as part of the build process but automated runs need to be introduced.  A Sage instance is required in a known, rewindable state is required for these tests to work.  

# Assumptions

1. Legacy operations are not critical as patches are rarely applied.  Access to the output \- the installers \- is critical.
2. Effort on making Legacy operations resilient is best focussed on upgrading software to .net.  This is because a few components of the Legacy operation are no longer supported and any attempt to replicate them may prove difficult.
3. The dependency on C1 Components and Installshield will not be changed within the scope of this project. Both may be possible, particularly Installshield, but may lead to the scope going out of control.

# Project Scope

## Legacy Operations

Legacy operations should remain on the "Development Server" indefinitely.  Plans should be put in place to provide alternatives that can be accommodated within the newer infrastructure. 

However, it should be possible to place the server hyper on the cloud as a PAAS hosted server.  Issues may occur but it is hoped that these can be rectified in a timely manner. This server will require an full Installshield licence as definitions will be maintained on it.  It will have to be accesses via RDP.  It is not excepted to require access to Codis network resources nor will is offer shares.   

Built legacy installers can be downloaded each time and copied manually to the new SharePoint storage.  This is likely to be so infrequent as to make the inconvenience of this process not an issue.

A DR plan will be needed for the server, whether onsite or PAAS hosted.

## Non\-Legacy Operations

### Installshield and Component One

- All Installshield process will have to run on self\-hosted agents that have either the Installshield or the standalone build agent capability.  As the "Development Server", preserved for Legacy Operations will have the full version available, this should be used.  Another self\-hosted agent on another server could have the standalone licence.
- Component One will also require a self\-hosted agent.  This can be the same or different agents as the Installshield agents.

### Remote Powershell and File System access

### 

Remote Powershell and accessing internal shares are likely to fail or be difficult to support in any PAAS hosted server or SAAS infrastructure.  To help enable such a move:

- All resources that are on local or shared onsite servers will have to be moved to resources available to cloud based processes.  These can be Azure DevOps hosted git repositories, packages or SharePoint hosted shares.  This will have the additional benefit of bringing key resources under source control.

### Test Systems

For Sage 1000 MS SQL can be added as capabilities to the servers running the agents and a restore operation could be added to the pipelines running the scripts (although currently this isn't required).   However, apart from the possibilities of a conflict by having test run in parallel, only a single instance of the test databases is required providing all agents can access it.  This architecture can be tested by creating a test instance of SQL in a PAAS or SAAS (or between) cloud service. Pipelines could be amended to try to access these services.  However, it should be remembered that test performance is likely to degrade considerably if the data access from the agent to the SQL instance is slow.  

For Sage 200, a full Sage instance is required.  Access to Sage 200 services is via https.  Adding this capabilities to the servers hosting the self\-hosted agents is not desirable as it considerably complicate the DR process and burden those servers' resources.   It may be possible to host a standard test instance on a PAAS or SAAS cloud service and to access it from the agents.  It is not clear whether establishing whether this works should be within scope for this project, given that the Sage 200 automated tests are not operational at the moment.

### Agents

As mentioned, self\-hosted agents continue to be required.  However, it should be possible to have at least two agents on different servers available.  The rationalisation of resources already described should make the construction of the second server or recovery of either server more straightforward, simplifying the DR plan.

As the critical path DR will depend on these self\-hosted agents being made available,  the only incentive for using externally hosted agents is to alleviate strain on the self\-hosted agents and to encourage the habit of constructing pipelines that are self\-sufficient.  Access to externally hosted agents is limited with charges being applied once limits are breached, which somewhat runs against the idea of resilient automated processes, some of which are intentional ran as often as possible.  

## Migration Plan

A second DevOps server has been created with minimum capabilities available.  It has an agent CD01SR16105 on it.  

Builds and releases will be rationalised to minimize the capabilities expected of the agents, and to not use shared or local folders or attempt remote Powershells.

Agent CD01SR16105 can be used to test whether this is successful (although this will not test whether shared resources are accessed).  Capabilities will be added to CD01SR16105 only if they are thought to be absolutely necessary.  The Installshield standalone agent will be added.

Once all critical builds and releases are shown to function on agent CD01SR16105,  a DR plan for CD01SR16105 must be established.  Then Development server can be migrated to a PAAS infrastructure and tested. 

After this, CD01SR16105 could be migrated to a PAAS infrastructure as well.
