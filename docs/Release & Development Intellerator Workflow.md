---
title: Release & Development Intellerator Workflow
tags: []
description: D iscussed below is the workflow while making a releas e. The live repository
  has 2 branches development and release. Any changes made are pushed to…
created: '2023-07-06'
modified: '2023-07-06'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Release%20&%20Development%20Intellator%20Workflow.aspx
---

Discussed below is the workflow while making a release. 

- The live repository has 2 branches development and release.  Any changes made are pushed to the Development branch. The development branch is also known as 'Pre\-release' and has the most updated form of the dashboard. The release branch has the recent version that the customer has.
- Any bugs spotted in Pre\-release version should be sorted by creating a ticket in 'To Do' in DevOps and then dragging it to 'Doing' when work is started and finally pushed to the Development branch once the work is completed.
- Changes or bug fixes in development branch are pushed to 'Release' branch once the changes are reviewed and approved.
- Any new changes found during review will again be posted as a ticket in DevOps and pushed to development branch once completed.
- Any new changes added during the review will be pushed to the Development branch and will wait for the next review to be pushed to the release branch.

Shown below is a work flow chart showing the position of development and release branches at various stages.  

[image wiki \-release and development workflow.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Release%20%26%20Development%20Intellator%20Workflow/image%20wiki%20-release%20and%20development%20workflow.png)
