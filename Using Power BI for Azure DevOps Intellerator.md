---
title: Using Power BI for Azure DevOps Intellerator
tags: []
description: The Boards section of DevOps has three columns 'To Do', 'Doing' and 'Done'.
  Upon starting a new project in Power BI that relates to an existing…
created: '2023-07-05'
modified: '2023-08-09'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator.aspx
---

The Boards section of DevOps has three columns 'To Do', 'Doing' and 'Done'. 

Upon starting a new project in Power BI that relates to an existing dashboard follow the steps below:

1. Create a new ticket in the 'To Do' list by giving a short and reasonable description of it and fill in the 'Days remaining' space. Choose 'Save \& Close' to find the ticket in the 'To Do' list.
2. When ready to begin work on it drag it to 'Doing' column.
3. Select the moved ticket from 'Doing' list and choose 'create a branch'.      [create a branch.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/create%20a%20branch.png)                 Or, you can choose the 3 dots on upper right corner and select 'New Branch' option to create a branch.
4. The Create Branch box dialogue box will be displayed.   [Create a branch dialogue box.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Create%20a%20branch%20dialogue%20box.png)                     Enter the
name of the branch in the format of : Ticket No.\\2\-3 word description.                                         (Note:
the description cannot contain a space ‘’. Use ‘\-‘  where a space is intended.)       After filling the
details choose ‘Create branch’ option.  You can find the branch linked in the ticket.
5. Go to the Git graph in VS Code (make sure you have cloned the repository) and click fetch to see your newly added branch.       [Fetch.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Fetch.png)
6. Double click the newly created branch to open the 'Check out branch' dialogue box. You can choose the default name or add a new name and click on 'Checkout Branch' option.
7. . All the work will now be done in the new branch. Once the changes are made and you have saved them, go to Git graph and commit the changes after adding a short description.   [Commit.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Commit.png)
8. The branch you are working on is ahead of the main branch. To add the changes to the main /origin branch 'Push' up the changes.
9. Go to Files section of your branch in Repos of DevOps
and click refresh. A message of updated branch and an option to create ‘Pull
Request’ can be found.   [Pull request.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Pull%20request.png)                                                              You can also find the create pull request option in
your ticket. This allows the reviewer to review your changes and pull it to the
development branch.    [Pull request\-2\.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Pull%20request-2.png)                                                          Complete the Pull request form by adding a Title
mentioning your change and a description if needed and add in the Reviewers
name. When done click on ‘Create’.[Pull request form.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Pull%20request%20form.png)

10\. When the changes are reviewed by the Reviewer they
are merged to the Development branch and the earlier branch is deleted. 

Note:


	1. Always
	push only completed changes/tasks to the Development branch.
	2. You
	can manually create a Pull request by selecting Pull request from Repos          [Pull request\-repos.png](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Using%20Power%20BI%20for%20Azure%20DevOps%20%20Intellerator/Pull%20request-repos.png)

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-


> ## Steps To Install GIT on your P.C[Git Installation steps.docx](https://codislimited.sharepoint.com/sites/Wiki/Documents/Git%20Installation%20steps.docx)

        \-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
         Pre\-requiste of PR:  
  
         1\. sync ticket branch and dev with origin  
          (usually involves pushing the ticket branch and pulling the dev, but the blue sync button will do it automatically. Also if the origin ticket branch is in an                   incorrect position, you will of course need to correct it first, which usually involves setting your local ticket branch to the correct position and force                         pushing).  
          2\. Branch locally at dev, call it temp, checkout branch  
   
         3\. Merge ticket branch into temp branch, choosing the changes in your work that you want to include.  
             Dont just accept all staged changes, go through each change and choose what to stage/unstage. Don't just glance at each file, use the up down arrows                 to jump to each change. This step involves you reviewing which changes you want to keep in your work, at the same time as merging into the latest dev                 branch, which might involve conflicts, so take your time.  
   
         4\. Checkout the ticket branch and off merge temp branch into ticket branch.  
             You may need to select the temp branch for viewing in git graph if you can't see it.  
   
         5\. Delete temp, push ticket branch, Create PR
