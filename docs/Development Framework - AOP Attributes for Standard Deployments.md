---
title: Development Framework - AOP Attributes for Standard Deployments
tags:
- Development
- AOP
description: Below is a typical configuration for a standard deployment. 1 2 3 4 5
  6 7 8 9 < object id = "ApplyPermissionsIfAttribute" type =…
created: '2017-01-16'
modified: '2017-01-24'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Development%20Framework%20-%20AOP%20Attributes%20for%20Standard%20Deployments.aspx
---

Below is a typical configuration for a standard deployment.



| 123456789 | `<``object` `id``=``"ApplyPermissionsIfAttribute"` `type``=``"Spring.Aop.Support.AttributeMatchMethodPointcutAdvisor, Spring.Aop"``>` `<``constructor-arg` `name``=``"advice"` `>``<``object` `name``=``"StandardAPIAdvice"` `type``=``"Codis.Excelerator.Sage200.Standard.Core.StandardSage200APIAdvice, Codis.Excelerator.Sage200.Standard"` `/>``</``constructor-arg``>``<``property` `name` `=``"CheckInterfaces"` `value``=``"true"` `/>``<``property` `name``=``"attribute"``value``=``"Codis.API.Types.Attributes.CompanyPermissionRequiredAttribute,Codis.API.Types"` `/>``</``object``>` |
| --- | --- |

and



| 12345678910111213141516 | `<``object` `type``=``"Spring.Aop.Framework.AutoProxy.AttributeAutoProxyCreator , Spring.Aop"``>``<``property` `name``=``"AttributeTypes"``>``<``list``>``<``value``>Codis.API.Types.Attributes.CompanyPermissionRequiredAttribute, Codis.API.Types</``value``>``</``list``>``</``property``>``<``property` `name``=``"InterceptorNames"``>``<``list``>``<``value``>ApplyPermissionsIfAttribute</``value``>``<``value``>CacheResultByCompanyInterceptor</``value``>``</``list``>``</``property``>``<``property` `name``=``"CheckInherited"``>``<``value``>true</``value``>``</``property``>``</``object``>` |
| --- | --- |

The BusinessAPI class should be inherits by the API class. This applies the CompanyPermissionRequiredAttribute to the whole class.



| 12 | `<CompanyPermissionRequired()>``Public` `MustInherit` `Class` `BusinessAPI` |
| --- | --- |

The second configuration means that the API class is proxied and two interceptors ApplyPermissionsIfAttribute and CacheResultByCompanyInterceptor are used.

The first page of the configuration defines the ApplyPermissionsIfAttribute interceptor and a AttributeMatchMethodPointcutAdvisor. This looks for the attribute CompanyPermissionRequiredAttribute on **methods** and invokes the StandardAPIAdvice interceptor object if found.
