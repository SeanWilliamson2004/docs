---
title: The Purpose of Testing New Releases
tags:
- Support
- Development
- Testing
- Release
- TFS
description: '"The purpose of testing new releases" is to ensure that the new release
  goes out and is an improvement over the existing version. We have test plans…'
created: '2017-01-27'
modified: '2022-11-25'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/The%20Purpose%20of%20Testing%20New%20Releases.aspx
---

**"The purpose of testing new releases" is to ensure that the new release goes out and is an improvement over the existing version.** 

We have test plans in TFS now \- the following is a general list of principals, to guide our testing in future. 

When we test a new release we are checking the following and logging all activity in TFS, both positive findings and negative. 

1\. That the known issues are now fixed.

2\. The basic functioning of Excelerator is the same as they were before. For example download, upload and browsing data.

3\. Extra functions for example designer, editing an existing template and adding or removing options.

4\. If we notice and differences we must quantify them and give steps a how to recreate.

5\. If the test we are doing has a specific purpose, for example testing office 2016 as opposed to office 2013, or 32 bit as opposed to 64 bit. Then we must also establish if the issue found is related to the purpose of the testing. 

- (a) If it is related put the details in the TFS case that you are testing on.
- (b) If it is not related start a new TFS case.
