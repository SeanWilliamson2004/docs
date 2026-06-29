---
title: Simplifying SQL
tags: []
description: 'SCENARIO 1: Subquery to GROUP BY --Unsimplified query SELECT StockItem.ItemID,
  ( SELECT SUM( MovementBalance.OpeningStockLevel -…'
created: '2023-03-27'
modified: '2023-03-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Simplifying%20SQL.aspx
---

SCENARIO 1: **Subquery to GROUP BY**  

\-\-Unsimplified query  

  SELECT

     StockItem.ItemID, 

        ( 

          SELECT 

            SUM( 

                 MovementBalance.OpeningStockLevel \- MovementBalance.StockLevelIssued

                  )  

             FROM

              MovementBalance 

          INNER JOIN BinItem ON BinItem.BinItemID \= MovementBalance.BinItemID  

          WHERE

              ( 

            (MovementBalance.MovementBalanceTypeID \= 0\) 

             OR (MovementBalance.MovementBalanceTypeID \= 2\) 

             ) 

         AND (BinItem.ItemID \= StockItem.ItemID)

      ) AS Quantity

  FROM StockItem;  

   Here in this code we are initially using the SUM function and then joining a table further by adding a subquery using WHERE and then filtering using the AND function which all is then aliased as Quantity. Instead this can be achieved by initially extracting all tables and joining them using a JOIN function and using an IIF to give the conditions, and finally using the GROUP BY statement.  

   \-\- This equals  

  SELECT 

    StockItem.ItemID, 

    SUM( 

        IIF( 

            (MovementBalance.MovementBalanceTypeID \= 0\) 

            OR (MovementBalance.MovementBalanceTypeID \= 2\), 

            MovementBalance.OpeningStockLevel \- MovementBalance.StockLevelIssued, 

            0 

          ) 

       ) AS Quantity   

              FROM   

                       StockItem   

                      LEFT JOIN BinItem ON BinItem.ItemID \= StockItem.ItemID 

                      LEFT JOIN MovementBalance ON BinItem.BinItemID \= MovementBalance.BinItemID 

     GROUP BY StockItem.ItemID  

SCENARIO 2 : **Coalesce**  

 \-\- unsimplified query

   SELECT 

     COALESCE( 

           COALESCE(thing1, 0\) \+ COALESCE(thing2, 0\) 

        , 0\)

    FROM 

      SomeTable;  

       In this case the Outer coalesce is not required as the Sum of 2 coalesces used here will never give a null value. Hence the outer coalesce can be removed.  

  \-\- this equals

     SELECT 

     COALESCE(thing1, 1\) \+ COALESCE(thing2, 0\)

     FROM 

          SomeTable;
