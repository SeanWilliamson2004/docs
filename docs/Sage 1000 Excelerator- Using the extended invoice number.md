---
title: 'Sage 1000 Excelerator: Using the extended invoice number'
tags: []
description: Using the extended invoice number Project DA0904 offers the possibility
  of having an invoice number of up to 30 characters - the payment reference.…
created: '2019-10-30'
modified: '2019-10-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%201000%20Excelerator%20Using%20the%20extended%20invoice%20number.aspx
---

Using the extended invoice number

Project DA0904 offers the possibility of having an invoice number of up to 30 characters \- the payment reference.  In Sage and  Excelerator, this extended invoice number is entered into another field. (Payment Reference under the DA0904 ranges in Excelerator, and the  Extended Invoice number in Sage).  If the system key PLPAYREFU is YES then this item number must be unique for a given supplier, and the regular item number can be left blank. (It is autopopulated).

  
 

Excelerator has extended this functionality.  Provided that DA0904 project is activated, and PLPAYREF and PLPAYREFU system keys are set to YES, and if the system key CODPLEXTNO is added and set to YES, then the regular item number can hold up to 30 characters.  The payment reference number itself should not be used.  The extended item number is transferred to the payment reference data field by Excelerator, and will appear in the Extended Invoice number in Sage.
