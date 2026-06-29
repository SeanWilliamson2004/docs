---
title: New Validation Engine
tags:
- Development
- Validation
description: This page is intended for developers only. It describes how to use the
  new Validation Engine. Overview The spring validation engine cannot be used as…
created: '2017-01-27'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/New%20Validation%20Engine.aspx
---

**This page is intended for developers only. It describes how to use the new Validation Engine.**

## Overview

The spring validation engine cannot be used as Spring.Core.dll is not allowed by the Sage validation rules. Base classes for a new validation engine have been added to the Codis.Sage200\.Server assembly. These classes work in a similar way to the Spring validation engine, to make porting easier. However, they try to improve in certain key areas. 

Validation is carried out in groups of Validation objects. 

## Validator Groups

Groups are defined in classes that inherit from DTOValidatorGroup. The list of validators to be validated in a group are defined in a list in the validator class. The list can include other validation groups. You can choose not to use the list and override the InternalValidate method. 

## Validators

Validators should inherit from DTOValidatorBase(of T). T is the type of the DTO being validated. 

Implement the validation by overriding the InternalValidate method. The first parameter , ObjectToValidate should be of the type T. 

AddMessage can still be used to add validation failure messages. However, the new validation engine does not support the use of literal strings for property names. Instead, actually property values must be used. As such, the BaseProperties property is no longer supported. Instead, set the MessageParameters protected property to the actual values in the InternalValidate method.

| ``` 1
 2
 3 ``` | ``` Protected Overrides Function InternalValidate(objectToValidate As LedgerDetailDTO) As Boolean
         Dim valid As Boolean = True
         MessageParameters = {objectToValidate.TaxCode, objectToValidate.TransactionAnalysis}.ToList
  ``` |
| --- | --- |

Or just pass an array of values to AddMessage as a parameter. 

Validators that use warning should inherit from the DTOWarningValidator base class. The IsWarning property is no longer used. 

The IgnoreWarning method is still available and it works in much the same way.
