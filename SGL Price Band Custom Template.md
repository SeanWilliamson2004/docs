---
title: SGL Price Band Custom Template
tags: []
description: SGL Price Band Template.xlsm Attached file is the custom template for
  Price Bands for Souther Group Limited. This was created and tested on 3.2.170…
created: '2021-07-19'
modified: '2021-12-15'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/SGL%20Price%20Band%20Custom%20Template.aspx
---

[SGL Price Band Template.xlsm](https://codislimited.sharepoint.com/sites/Wiki/Support/Backup/Rhys%20Bhan/SGL%20Price%20Band%20Template.xlsm)  


  
Attached file is the custom template for Price Bands for Souther Group Limited.  


This was created and tested on 3\.2\.170 version of Ex S200\.

The template has a Pivot table and some VBA codes working together with External object of Codis Excelerator to extract data from Database usinng views and saving them to Sage.

  


Sql details for the template  


username \- Codisdb  


password \- PencilRestriction42  


  


This template needs a Database view to run  


  


Customer\_SOP\_PB\_Vw  


  


SELECT        dbo.SLCustomerAccount.CustomerAccountShortName, dbo.SLCustomerAccount.CustomerAccountNumber, dbo.SOPOrderReturnLine.ItemCode, dbo.SOPOrderReturnLine.LineQuantity,                          dbo.SOPOrderReturnLine.LineTotalValue, dbo.SOPOrderReturnLine.UnitSellingPrice, dbo.SOPOrderReturnLine.PromisedDeliveryDate, dbo.StockItem.Name AS StockDescription, stockitem.ItemID,                          COALESCE (spc.price, 0\) pricebandpriceFROM            dbo.SLCustomerAccount INNER JOIN                         dbo.SOPOrderReturn ON dbo.SLCustomerAccount.SLCustomerAccountID \= dbo.SOPOrderReturn.CustomerID INNER JOIN                         dbo.SOPOrderReturnLine ON dbo.SOPOrderReturn.SOPOrderReturnID \= dbo.SOPOrderReturnLine.SOPOrderReturnID INNER JOIN                         dbo.StockItem ON dbo.SOPOrderReturnLine.ItemCode \= dbo.StockItem.Code LEFT JOIN                             (SELECT        \*                               FROM            (SELECT        cp.PriceBandID, s.Code, s.ItemID, sp.DateTimeUpdated, sp.Price, c.CustomerAccountNumber, ROW\_NUMBER() OVER (partition BY s.itemid, c.customeraccountnumber                                                         ORDER BY p.datetimecreated DESC) rnk                               FROM            SLCustomerAccount c INNER JOIN                                                         SLCustomerPriceMapping cp ON cp.SLCustomerAccountID \= c.SLCustomerAccountID INNER JOIN                                                         PriceBand p ON p.PriceBandID \= cp.PriceBandID INNER JOIN                                                         StockItemPrice sp ON sp.PriceBandID \= cp.PriceBandID INNER JOIN                                                         StockItem s ON s.ItemID \= sp.ItemID                               WHERE        p.IsActive \= 1\) fWHERE        f.rnk \= 1\) spc ON spc.CustomerAccountNumber \= SLCustomerAccount.CustomerAccountNumber AND spc.ItemID \= StockItem.ItemIDWHERE        (dbo.SOPOrderReturnLine.LineQuantity \> 0\) AND (dbo.SOPOrderReturnLine.LineTotalValue \> 0\) AND (dbo.SOPOrderReturnLine.ItemCode IS NOT NULL) AND (dbo.SOPOrderReturnLine.ItemCode \<\> '');
