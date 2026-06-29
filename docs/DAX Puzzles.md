---
title: DAX Puzzles
tags: []
description: These puzzles are for your dax practice. The difficulty of these are
  rated out of 5 stars (5 being the most difficult). Unless otherwise stated, do…
created: '2023-02-10'
modified: '2023-05-04'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/DAX%20Puzzles.aspx
---

These puzzles are for your dax practice. The difficulty of these are rated out of 5 stars (5 being the most difficult). Unless otherwise stated, **do not use power query, DAX calculated columns or DAX calculated tables**. A puzzle file and an answer file is given for each, some with a link to an explanation.  

# Total Sales ⭐⭐

We have the following Orders and Products tables:  

![total sales.jpg](images/PublishingImages_Pages_DAX_Puzzles_total_sales.jpg)  

Write a **single** measure "Total Sales" which gives the value of the total sales (the unit price is is in the products table and the quantity ordered is in the orders table). You are **not** allowed to write more than one measure (everything must be in one measure), and you must not use DAX variables.   

[Puzzle \- Total Sales.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Puzzle%20-%20Total%20Sales.pbix)  

[Answer \- Total Sales.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Answer%20-%20Total%20Sales.pbix)  

# Top Store Manager ⭐⭐⭐

We have the following table: 

![Sales with other cat.jpg](images/PublishingImages_Pages_DAX_Puzzles_Sales_with_other_cat.jpg)  

Write a measure for the store manager that sold the most.

[Puzzle \- Top sales manager.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Puzzle%20-%20Top%20sales%20manager.pbix)  

[Answer \- Top sales manager.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Answer%20-%20Top%20sales%20manager.pbix)  

# 

# Top Sales Manager 2 ⭐⭐⭐⭐

We start with the **answer** for the Top Sales Manager puzzle. The measure "Top Sales Manager" works in a card, but if we add it as a column in the table it looks like this:  

![Top sales manager 2 q.png](images/PublishingImages_Pages_DAX_Puzzles_Top_sales_manager_2_q.png)  

Correct the measure so that the top sales manager Debby is repeated on every row, like this:  

![Top sales manager 2 a.png](images/PublishingImages_Pages_DAX_Puzzles_Top_sales_manager_2_a.png)  

Try to change the original measure as little as possible.   

[Puzzle \- Top sales manager 2\.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Puzzle%20-%20Top%20sales%20manager%202.pbix)  

[Answer \- Top sales manager 2\.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Answer%20-%20Top%20sales%20manager%202.pbix)  

[Explanation \- Top Sales Manager 2](DAX Puzzle Explanation - Top Sales Manager 2.md)  

# 

# Subtotal groups (SQL Puzzle) ⭐⭐⭐⭐⭐

Run this query on any test database, it will create a new table.  

[Create subtotals table.sql](https://codislimited.sharepoint.com/sites/Wiki/Documents/Create%20subtotals%20table.sql)  

The first few rows will look like this:  

![Subtotal groups excel preview.png](images/PublishingImages_Pages_DAX_Puzzles_Subtotal_groups_excel_preview.png)  

Write a select query on this table that should give 2 columns: Subtotal Row No and Value Row No. If the subtotal group \= 0, then this is a "Value Row". If the subtotal group is \> 0, then this is a "Subtotal Row" and should be matched with every value row before it, up to the previous subtotal row of the same or higher subtotal group.  

For example, the first subtotal is row no 3 as the subtotal group is \> 0\. Row 3 is matched with rows 1 and 2 above it. Row 5 is matched with row 4 but no other rows, because row 3 is a subtotal of an equal or higher group (group 1\). Row 6 is matched with rows 1 to 5, as all the subtotal groups above row 6 is less than 2\. Row 10 is matched with 7,8 9, all the way until row 30 which is matched with 25, 26, 27 and 29\. The final SQL output should be the following:  
[sql output.xlsx](https://codislimited.sharepoint.com/sites/Wiki/Documents/sql%20output.xlsx)  

This puzzle is quite tough, and so far I have had to use temporary tables. The answer is here:  

[Subtotal puzzle answer.sql](https://codislimited.sharepoint.com/sites/Wiki/Documents/Subtotal%20puzzle%20answer.sql)  

# 

# Pie chart with "Other" category ⭐⭐⭐⭐⭐

We have the following table:

![Sales with other cat.jpg](images/PublishingImages_Pages_DAX_Puzzles_Sales_with_other_cat.jpg)  

Make a pie chart of sales by store name, except the bottom 20% of all sales should belong to the "Other" category. Like so:  

![Sales with other pie.jpg](images/PublishingImages_Pages_DAX_Puzzles_Sales_with_other_pie.jpg)  

[Puzzle \- Sales with Other.pbix](https://codislimited.sharepoint.com/sites/Wiki/Documents/Puzzle%20-%20Sales%20with%20Other.pbix)

[Answer\- Sales with Other.pbix](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/DAX%20Puzzles/Answer-%20Sales%20with%20Other.pbix)
