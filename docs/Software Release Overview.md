---
title: Software Release Overview
tags:
- Support
- Release
description: This is a master page for the release process, giving an overview and
  collating other pages. Process Overview Agree that a release is needed.…
created: '2022-11-24'
modified: '2025-02-13'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Software%20Release%20Overview.aspx
---

This is a master page for the release process, giving an overview and collating other pages.  

## Process Overview

1. Agree that a release is needed.  Frequent releases will mean that Codis will quickly gain value from programming investment, and ensure that we can respond more quickly to sudden demand.
2. Open the S200 release in [Devops Release Management](https://dev.azure.com/codislimited/CodisDevelopment/_release?_a=releases&view=mine&definitionId=19).  Check that there aren't any previous releases that were not either completed or abandoned since the last completed release.  Releases that weren't completed probably should be abandoned.  If you know why they weren't completed, write this in the abandonment comments.
3. Start a S200 Excelerator release in [Devops Release Management](https://dev.azure.com/codislimited/CodisDevelopment/_release?_a=releases&view=mine&definitionId=19).  Ensure that the "Build Environment" and "Create Pre\-Release Notes" deployment steps execute.
4. When the "Create Pre\-Release Notes" deployment step is completed, view the InternalReleaseNotesXXXX (where XXXX is the release number) in the [Sage 200 Pre\-Test area](/sites/builds/Shared%20Documents/Forms/AllItems.aspx?viewpath=/sites/builds/Shared%20Documents/Forms/AllItems.aspx&OR=Teams-HL&CT=1646256712708&params=%7b%22AppName%22%3a%22Teams-Desktop%22%2c%22AppVersion%22%3a%2227/22010300411%22%7d&id=/sites/builds/Shared%20Documents/Pre-Test/S200Standard&viewid=136b23c9-2d50-43d6-a045-b7190ece9fb6).
5. Use these notes to create a test plan. (see [Planning for Testing a Release.aspx](Planning for Testing a Release.md)).  Assign test cases to be completed and assign them to be tested.
6. Perform the testing, which is best performed unless the DevOps Test Runner, as this integrates with DevOps.
7. Consider the impact of test failures.  If any regression or critical bugs are found then abandon the release being tested, noting the cause.  Create a new release (and this process returns to Step 2\).
8. If all tests pass, or all test failures are not considered significant, complete the release in Devops Release Management by approving the "Full Release" stage (Yasmin, Rohit or Sean can do this).  This will copy the release from the pre\-test area to the [Full Release area.](/sites/builds/Shared%20Documents/Forms/AllItems.aspx?viewpath=/sites/builds/Shared%20Documents/Forms/AllItems.aspx&OR=Teams-HL&CT=1646256712708&params=%7b%22AppName%22%3a%22Teams-Desktop%22%2c%22AppVersion%22%3a%2227/22010300411%22%7d&id=/sites/builds/Shared%20Documents/Release/S200Standard&viewid=136b23c9-2d50-43d6-a045-b7190ece9fb6)
- This Full Release stage will probably fail.   To get around this, edit the stage and remove the copy task.  Manually copy the msi file from the Pre\-Test area to the  [Full Release area](/sites/builds/Shared%20Documents/Forms/AllItems.aspx?viewpath=/sites/builds/Shared%20Documents/Forms/AllItems.aspx&OR=Teams-HL&CT=1646256712708&params=%7b%22AppName%22%3a%22Teams-Desktop%22%2c%22AppVersion%22%3a%2227/22010300411%22%7d&id=/sites/builds/Shared%20Documents/Release/S200Standard&viewid=136b23c9-2d50-43d6-a045-b7190ece9fb6).  The release area does not hold historical copies.  The file should have the version removed from its name so that there is a single file for each version of the product.   Note that we usually only update SPE2019 now.

10. Inform Raghu so that he can copy the release to the website.
11. Copy the ExternalReleaseNotes*XXXX*.html notes (*XXXX*is the release number)  from the pre\-test area onto the help .
1. Click on the release notes to open them.
2. Select Open\-\>Open In Text Editor from the top left\-hand corner.  
![EditReleaseNotes.png](images/PublishingImages_Pages_Sage_200_Software_Release_Overview_EditReleaseNotes.png)
3. Copy all the html.
4. Log into help.codis.co.uk as an editor.
5. Open the S200 Help **project**.
6. Open Release Notes under "Introducing Excelerator"
7. Add a new topic "Release XXXX" where XXXX is the release number.  Pre\-fix the automatic ID with S200\_
8. Edit the topic, and open the "Source" tab.  Paste the HTML from the release notes into the page.
9. Unlock and View.  Preview the resulting page to check it looks ok.

## See Also

| Creating and completing a test plan. | [Planning for Testing a Release.aspx](Planning for Testing a Release.md) |
| --- | --- |
| Azure Devops testing.  Overview of why to use Devops testing, what test cases and plans are, and how to execute a test using the test runner. | [Azure Devops Testing.aspx](Azure Devops Testing.md) |
| How WIs, builds, PRs and releases combine with releases in our Agile processes. | [ALM \- Software Release Procedures.aspx](ALM - Software Release Procedures.md) |
| Notes on how the release notes are generated. | [Release Notes.aspx](Release Notes.md) |
| How to add inline tests | [Azure Devops Inline Tests.aspx](Azure Devops Inline Tests.md) |
| Brief discussion regarding testing | [The Purpose of Testing New Releases.aspx](The Purpose of Testing New Releases.md) |
