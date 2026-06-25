---
title: Steps for Merging changes in Release branch
tags: []
description: 'There are two ways to merge : Using Git Commands Using Git Graph in
  VS Code Commands for option 1: git fetch --all git checkout development git pull…'
created: '2023-09-15'
modified: '2023-09-15'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Doing%20a%20release.aspx
---

There are two ways to merge :  


1. Using Git Commands
2. Using Git Graph in VS Code

Commands for option 1:  


git fetch \-\-all  
git checkout development  
git pull  
git checkout release  
git pull  
git merge development  
git tag \<1\.0\.4\> REPLACE THIS(1\.0\.4\) WITH THE NEW VERSION NO  
git push origin \-\-follow\-tags  
  
Steps for option 2:  
Lets take example from existing repository snapshot below.  
  
In the git graph we can see development branch is above Release branch as development is on top.  


1. Checkout development branch by double clicking on that and clicking checkout Branch and "then checkout and Pull".  
  
![checkout branch development.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_checkout_branch_development.PNG)  
  
![checkout branch development and pull.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_checkout_branch_development_and_pull.PNG)
2. Fetch by clicking as shown by ble arrow in snap below.  
  
![fetch for dev branch.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_fetch_for_dev_branch.PNG)
3. Checkout Release Branch with version number and sync or pull changes.  
  
![checkout release.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_checkout_release.PNG)  
  
![sync or pull release branch.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_sync_or_pull_release_branch.PNG)  
  
![release branch jumps above.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_release_branch_jumps_above.PNG)
4. Add tag  
  
![add tag at release branch.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_add_tag_at_release_branch.PNG)  
  
![add tag2.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_add_tag2.PNG)
5. Merge Development Branch into Release Branch  
  
![Merge development into release.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_Merge_development_into_release.PNG)  
  
![merge confirmation.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_merge_confirmation.PNG)  
  
You can see release branch jump next to development branch. Click Sync changes.  
  
![release after merge.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_release_after_merge.PNG)  
  
Add tag as below snap.  
  
![add tag after merge.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_add_tag_after_merge.PNG)  
  
![add tag after merge3.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_add_tag_after_merge3.PNG)  
  
![add tag after merge4.PNG](images/PublishingImages_Pages_Steps_for_Merging_Development_Branch_in_Release_branch_add_tag_after_merge4.PNG)  
  
Finally Development branch is Merged into Release branch.
