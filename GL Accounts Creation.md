---
title: GL Accounts Creation
tags:
- Sage X3
description: '1. Creation of General ledger accounts Transaction Code: GESGAC Description:
  General ledger accounts The setup function for accounts is used to…'
created: '2017-01-27'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/GL%20Accounts%20Creation.aspx
---

1\.       Creation of General ledger accounts 

**Transaction Code: GESGAC Description: General ledger accounts** 

The setup function for accounts is used to specify the characteristics of an account that will be used to post General and Analytical accounting entries. 

## Fields explanation:

Chart \- This field recalls the chart of accounts on which the account (general, analytical, both) will be created or to which they will be attached. Before creating an account, the attachment chart of accounts needs to be specified using the Chart button. 

Account \- Account number that is used to identify it in the chart of accounts. The codification of the account depends on the format and length options applied during the setup of the chart of accounts. If the account numbering with fixed length option is retained, the account numbers entered will automatically be completed with "0"s up to the length defined in the setup. 

Collective \- The option Collective can only be accessed if the box Collective account of the chart of accounts is checked. By checking this box, it indicates that the account will be associated with a BP. 

Short code \- Each account can have call code with two or four characters that will be used as a keyboard shortcut in entry mode (for entries and documents). This code is mandatory for collective accounts. The call code must start with a letter. This code must not be mistaken with the mnemonic set up in the record of the journal: • The call code of the journal is made of only one character (letter or number), • It is associated with an account and a particular journal. In this case of a control account, this field contains the control account. (For instance, C1 for a collective customer). 

Currency \- This is the bookkeeping currency. If the currency is specified, the entries are only assigned in this currency. If no currency is specified, every currency may be accepted upon entry. 

Active (Check box) \- This box is used to specify whether the current record must be activated or not: •       if this box is checked, the current record can be used in other records (documents, parameters, etc.) or during mass processing, •       if it is not checked, the current record is considered to be inactive and it cannot be selected. 

Classification – It is the Identifier of the account class, composed of one to ten alphanumerical characters. It is the account class by default associated with the current chart of accounts. This value comes by default from the setup of the chart of accounts. It is used to specify: •       the behavior of the closure processing with respect to the account (CFE or not) •       the sign of the account balance in the various reports and inquiries for the analytical accounts. The subdivision into classes enables the off balance\-sheet accounts to be distinguished from the others. Default accounts: 

Other COA \- Enter in this field the chart of accounts, other than the original one, on which the account will be open to tracking. 

Default account \- It is the default account that will be tracked on another chart. If this field is not assigned, the account of the 'target' chart will be tracked but without default association. When the current account is tracked on another chart, it is possible to combine it with a default account on the 'target' chart. This line is used to define the propagation rules of the current account to another chart. 

Account screening \- It is the default account that will be tracked on another chart. If this field is not assigned, the account of the 'target' chart will be tracked but without default association. When the current account is tracked on another chart, it is possible to combine it with a default account on the 'target' chart. This line is used to define the propagation rules of the current account to another chart. 

Mandatory entry \- The posting on an account can be compulsory or optional. 1\. If the field is set to "Yes", the tracking on the specified chart of accounts will be compulsory in journal/document entry. 2\. If the field is set to "Yes", the tracking on the specified chart of accounts will be optional in journal/document entry. 

**Path: Common Data  G/L Accounting tables  General  Accounts** 

## Controls Tab:

Recurring account \- A recurring task account (usually, a class four account) can be associated with the current account. The automatic balance function of recurring tasks is used to automatically close an account as a counterpart to the recurring task account associated with it. This field is used by the recurring task automatic function in order to know the account on which the recurring task closure journal must equilibrate. If this account is a collective account, the user will have to give the BP code corresponding to the following field. 

Recurring BP – If this account is a collective account, the user will have to give the BP code corresponding to the following field. Automatic variances \- During the matching of entries in currency, the user might notice an automatic difference of conversion on payment. This automatism can be deactivated for some accounts for which the difference of conversion has no consequence. This possibility is mainly useful for accounts that can be matched. 

Tax management \- For an account, there can be five different situations regarding the VTA: •       The account is "Submitted" i.e. it might receive postings that must be taken into account in order to determine the taxable basis at VAT declaration. The sales and purchase accounts must be parameterized as "Submitted". •       The account is "not submitted", i.e. it has no relation with the VAT. The employee expense accounts, depreciation expense accounts or VAT accounts to regularize or declare must be parameterized as "not submitted". •       The account is a "VAT account', i.e. it receives postings that must be taken into account in order to determine the tax amount to declare. •       The account is a "EEC VAT" account, i.e. it receives postings that must be taken into account in order to determine the tax amount to declare in other EEC country. •       The account is a "prepayment" account. 

Post tax \- If an account is parameterized as "Submitted", "VAT account", "EEC VAT" or "prepayment account", the user must indicate here the VAT type to declare. There can be eight types of VAT (the three following types are used for French VAT): •       Deductible on purchases of goods and services, •       Deductible on asset acquisitions, •       Collected on sales. 

Tax codes – If we check 'Tax management' as subjected, this field becomes mandatory to enter the Tax codes and will be used during creation of journal entries. 

Variance type – We need to select the required option based on the usage of the account. For ex:\- If the account is P\&L account and then we need to Profit and Loss in this field and to update the transactions automatically. 

## Miscellaneous Tab:

Matchable \- All general and/or analytical accounts can use the matching 

Summary reporting \- The centralization is used to obtain a subtotal of the entries (sorted by journal) during the printing process of the general ledger. 

Carry forward in currency \- This witness defines the management rule to be applied to the carry forward entries, this means that the account class must be checked Carry forward entries. If it is activated, the carry forward entries are generated in currency. If not, the carry forward entries are generated in the bookkeeping currency of the ledger. 

Subject to discount – If we check this field, we need to specify the discount during creating the transactions with this account. 

Fixed asset tracking \- This checkbox must be checked in order to authorize the use of the accounts on assets and expenditures that are managed in the Assets module. 

Expense creation – This checkbox can be modified only if the Fixed asset tracking it activated. 

Accounting nature \- This field must be entered when the Tracking of assets is active. It is used to enter the accounting nature associated with the account 

## Analytical Tab:

Budget tracking \- Budget tracking can be used if and only if the account is attached to analytical ledger that can be budgeted. Checking this box gives the authorization for budgetary entry on this account. 

Temporary distribution \- The allocation key is used to define the allocation conditions of the annual budget, by assigning a weighing coefficient to each month. If the field is left empty, the same coefficient will be assigned to every month. 

Non\-financial unit entry \- The value posting, either analytical or budgetary, can be complemented by a quantity posting, on the basis of the non\-financial unit associated with the analytical account. The "NFU entry" flag must be activated. 

Non\-financial unit \- The quantity entered for each accounting document is expresses in this unit if applicable, the default value given to this unit will be used for the automatic calculation of quantities upon any entry of documents or BP invoice or in budget entry mode. 

Default value \- The standard value indicated here is used to pre\-initialize the quantity as a function of the amount or vice versa. 

Distribution key \- The analytical distribution codes are used to automatically distribute the amount of an accounting posting line over several analytical lines according to weighting factors and this, via a single entry. 

## Dimensions:

Dimension type \- This field is used to enter or select any analytical dimension type parameterized in the database. By default, if the account is subject of a screen defined in the chart of account, the loaded dimension types' codes come from the associated chart of accounts' setup. This list can be modified. If a dimension type is declared on this list, it means that the account is tracked on this dimension type. On the contrary, if a dimension type is not declared on this list, it means that the account won't allocate it. 

Dimension \- It is possible to specify for each dimension type a default dimension that will be submitted on entering a posting or a document in this analytical account.
