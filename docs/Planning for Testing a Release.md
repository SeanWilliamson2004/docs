---
title: Planning for Testing a Release
tags:
- Testing
- Release
description: This document describes how to create and complete a test plan. Process
  Overview The aim of the planning is to create Devops Testplan that includes…
created: '2022-08-11'
modified: '2022-11-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Planning%20for%20Testing%20a%20Release.aspx
---

This document describes how to create and complete a test plan.    

## Process Overview

The aim of the planning is to create Devops Testplan that includes all test cases or other steps that have to be completed before the release can be completed.    

**In planning to test a release some pragmatism is required.  An over\-cautious approach might not be proven to be a problem in terms of bugs in a release, but it can cause significant delays in releases, leading to poorly tested ad\-hoc per\-customer releases.**  

This is why test plans are needed.  Always taking the safety\-first approach and testing everything is not feasible so targeting testing is required, and working collaboratively on those tests requires a shared plan.    

The processes to create and complete a test plan are:  

1. Create a new test plan for a release.  (See "Building the Test Plan" below.
2. Examine the release notes that are created by the first stages of the release.  (See [Sage 200 Software Release Overview.aspx](Software Release Overview.md) and "Identifying Work Items Included in a Release" below.)  These notes tell us the work items that are included in a release.
3. Ensure that all work items **that are included in the release notes** have test cases or good reproduction notes or acceptance criteria associated with them.  Where there aren't test cases or the test cases aren't complete, placeholder inline test cases (see [Azure Devops Inline Tests.aspx](Azure Devops Inline Tests.md)) can be added and the test cases assigned to support staff to complete.
4. Add these test cases or other tests to the test plan to ensure that each work item is tested.
5. Evaluate the possibility of regression bugs being caused that will not be picked up by testing the work items.  Usually, programmers are best placed to do this.
6. Expand the scope of the testing to try to cover any areas not tested by testing work items but where regression bugs may appear.  This could be done by adding smoke tests or more detailed tests in the area that you are concerned may be destablised.
7. Once all test cases and steps are complete, then the test plan is complete.  It may be possible to start testing individual steps before the whole plan is completed.

## Identifying Work Items Included in a Release

The S200 Excelerator release now includes a stage "Create Release Notes" that is run as the first stage.  This uses a DevOps extension [Generate Release Notes](https://marketplace.visualstudio.com/items?itemName=richardfennellBM.BM-VSTS-XplatGenerateReleaseNotes) to identify which work items' fixes are included in a release.  These are then filtered down to those work items that are for the 'Sage 200 Excelerator' or 'All Excelerator' product groups.  The output is copied to the Prerelease area.  [An Example](/sites/builds/Shared%20Documents/Forms/AllItems.aspx?viewid=136b23c9-2d50-43d6-a045-b7190ece9fb6&viewpath=/sites/builds/Shared%20Documents/Forms/AllItems.aspx&OR=Teams-HL&CT=1646256712708&params=%7b%22AppName%22%3a%22Teams-Desktop%22%2c%22AppVersion%22%3a%2227/22010300411%22%7d&id=/sites/builds/Shared%20Documents/Pre-Test/S200Standard/ReleaseNotes3.3.51-2.html&parent=/sites/builds/Shared%20Documents/Pre-Test/S200Standard).  

This stage can be "redeployed" to generate the report again if the Work Items need correcting.  

Note: If the release completes and becomes a full release, then the release notes can be used to create a release notes page on the help site.  The release notes source can be viewed and the code for the first two tables can be copied to the "Source" editor in the help.  

## Building the Test Plan

A new test plan should be created for a new release.  

The test plan settings should be changed to select the build being tested.  

![SelectReleaseForPlan.png](images/PublishingImages_Pages_Planning_for_Testing_a_Release_SelectReleaseForPlan.png)  

Other test suites from other test plans can be imported :  

![ImportTestSuite.png](images/PublishingImages_Pages_Planning_for_Testing_a_Release_ImportTestSuite.png)  

So a standard test plan for e.g. S200 Excelerator smoke tests can be kept.  

## Testing Enhancements and Bug Fixes

Enhancements and bug fixes are defined in Work Items.  The User Story Work Items have acceptance criteria and Bugs have reproduction steps.  Both of these can be extended into test cases.  Test cases can be beneficial as they provide a detailed description of the expected functionality.  However, the work involved in defining those tests can be considerable, and the tests may end up being too restrictive because of limited time.  They can also be limited by the test case author's pre\-conceived ideas of how the change should work.  So **do not hesitate to add some exploratory testing** (https://www.atlassian.com/continuous\-delivery/software\-testing/exploratory\-testing) to the plan.  It is harder to document exploratory testing, but recording videos can be one way.  You can go off plan during testing with some exploratory testing but bear in mind that the plan has to be completed.  

## Regression Testing

This can be harder to define.  https://testfort.com/blog/regression\-testing\-how\-when\-and\-why\-you\-should\-do\-it describes the challenges well.  It defines *Local Regressions, Remote Regressions, and Unmasked Regressions.*

Checking for *Local Regressions* as a result of a change should form part of the testing of that change, as defined in the WI.

### Checking for Remote Regressions, and Unmasked Regressions

There is no right way to do this.  Testing as much as possible in as much depth as possible will provide the best protection against these, but takes time and resources.  

One approach is to try to ensure that there are no glaring failures in the software and to also try to anticipate where regressions may occur and test these areas.  i.e:  

- Smoke Tests
- Targetted tests

Smoke Tests can be a list of test cases attached to a plan.  These can be imported into the current plan.  
Targetted tests can be based on anticipating bugs introduced by code changes.  The scope of the code changes can be evaluated from the Work Items.  But this will always be an approximation.
