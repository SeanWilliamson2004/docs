---
title: Creation of Dimension types & Dimensions
tags:
- Sage X3
description: '1. Creation of Dimension types Transaction Code: GESDIE Description:
  Dimension Types This function is used to create the Dimension types and linked…'
created: '2017-01-25'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Creation%20of%20Dimension%20types%20&%20Dimensions.aspx
---

# 1\. Creation of Dimension types

**Transaction Code: GESDIE       Description: Dimension Types** 

This function is used to create the Dimension types and linked to dimensions. Dimensions are typically used to represent such items as departments, locations, regions and product lines. 

• A maximum of 20 dimension type can be defined. • These dimensions are shared across all companies defined within a Folder. • The values for a dimension type code are defined using the Dimensions task, and a value can be an amount or quantity. 

We can enter a maximum length of 15 at the Dim view format field. • We must enter the dimension length followed by either \# (numeric only), A (alpha characters only), or c (alphanumeric). • For example, 10A stands for a maximum length of 10 and you can only enter alpha characters as the account number (e.g. ARACCT). • It is important to note, some reports may not display the entire 15 characters if using the maximum length due to space limitation, font, and/or printer used. 

## Fields explanation:

Dim type code – We have to specify the THREE letter character and the description to identify the dimension type. 

Column header \- By default the short title, the long title or the column header of a data are recorded (on creation/update) in the connection language of the user. 

Dim view format \- This zone is used to define the coding format of the analytical dimensions and it can take values 'c' for alphanumeric characters and '\#' for numeric characters. 

## Flags:

Automatic creation \- This parameter is used to process the generation of the automatic journals or within the framework of the interfaces. 

No carry\-forward entry \- The data entered in a dimension type is purged at the end of the fiscal year using a "reset to zero (RTZ)" process. If the No carry\-forward entry flag is not checked, this purging can be avoided and all the analytical dimensions are carried forward from one period to another. 

Change final entries \- If this box is checked, the postings sorted as final can be modified on journal entry at analytical level, without having to reopen the period. The processing designed to modify the final postings works with the CNTANA parameter. 

Entity \- If a dimension view is flagged 'Entity", this means that it is dedicated to the "Operating Budgets" module. Implementing this module implies that the budget codes being used are set up. 

Envelope \- If a dimension view is flagged 'Envelope", this means that it is dedicated to the "Operating Budgets" module. Implementing this module implies that the budget codes being used are set up. 

**Path: Parameters  Organisational structure  Dimension type** 

## Miscellaneous dimensions tab:

The analytical dimensions are used to save analytical entries. 

# 2\. Creation of Dimensions

**Transaction Code: GESCCE       Description: Dimensions** 

This function is used to create the Dimensions. We can define an unlimited number of dimension values for each dimension type. 

Dimensions are typically used to represent such items as departments, locations, regions and product lines. The analytical dimensions may be considered as the "management centers" designed to aggregate the accounting information for analytical and budgetary purposes. Their nature depends on the analysis objectives used and upon which the concept of analytical dimension types is based. The dimensions are created for a given dimension type. There can be up to 9 dimension types independent from each other. Dimensions are associated with the analytical accounts. The dimensions are the reference element in the analytical management (posting of accounting documents) and budgetary management (entry). They are mainly used to carry out comparisons between the "actual" and the "budget". It can nevertheless be decided to restrict the entry of budget elements in an analytical dimension. 

## Fields explanation:

Dimension type – We need to select the dimension type by clicking 'Dimension type' button. 

Dimension – We need to provide the code and description to identify our dimension. It should not exceed TEN characters. 

Active – This box is used to specify whether the current record must be activated or not: 

• If this box is checked, the current record can be used in other records (documents, parameters, etc.) or during mass processing, 

• If it is not checked, the current record is considered to be inactive and it cannot be selected. 

## Controls block:

Carry forward \- If this is activated, it means that the balance of the current dimension is carried forward for those accounts to which entries have been posted. Furthermore it is used to carry forward all the entries of a dimension from one period to another. 

Budget tracking – If the field is checked, a budget can be built in this dimension. Using some dimensions can thus be reserved to the analytical accounting. They are mainly used to carry out comparisons between the "actual" and the "budget. 

Posting \- Select the Posting check box to indicate whether or not you can post entries to this dimension. Otherwise, it is strictly used for budget tracking. 

Other dimensions \- It is possible to initialize the value of a dimension type with respect to another. By specifying dimension types and associated dimensions, the current dimension can be used to initialize the dimension types concerned. 

Non\-financial unit \- This grid is used to define a set of non\-financial units and a (permanent) value assigned to the dimension for this unit. This information will be used by the allocation structure program. 

**Path: Common Data  G/L Accounting Tables  Analysis  Dimensions** 

## Pyramids Tab:

Principally used for reports and inquiries, the dimension pyramids are used to characterize the summary (roll\-up) level and order of the information to be retrieved. Their update is retroactive to the construction of the pyramids.
