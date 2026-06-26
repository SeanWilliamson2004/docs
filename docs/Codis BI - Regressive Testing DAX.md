---
title: Codis BI - Regressive Testing DAX
tags: []
description: Description Sometimes, when changes are made to the model or DAX in order
  to resolve a bug, it can inadvertently affect other functionalities in the…
created: '2024-01-02'
modified: '2024-01-02'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20BI%20-%20Regressive%20unit%20testing%20DAX.aspx
---

# Description

Sometimes, when changes are made to the model or DAX in order to resolve a bug, it can inadvertently affect other functionalities in the dashboard. Consequently, the dashboard might produce undesired results in calculations that were previously correct before those changes were implemented.  
  
Regression testing helps identify such errors, which is why it is recommended after every bug fix.# Guidelines

1. Keep unit tests as small as possible. Eg if the same test can be done on only 1 invoice, filter to only that 1 invoice.
2. Test one behaviour at a time, eg test the value after filtering on period, or test the value after filtering on product. Avoid mixing behaviours, eg filtering on period and product. About 10% of the tests can mix behaviours, but these are not unit tests, they are "integration" tests. The aim is that if a tests breaks, you know where to look in the DAX.
3. Before writing a measure, have it just return 0 or "". Write the test for the measure first, it should fail. Then write the smallest DAX which passes the test. Then you can add another test before adding more to the measure. Eg Consider a measure \- \[Can Drive], which is TRUE if the selected Person is over 18 and they are Alive, first write the unit test that a person over 18 can drive, it should fail. Make it pass by amending \[Can Drive] to return TRUE if the person is over 18\. Then add a unit test to check if \[Can Drive] is FALSE if the person is not alive. It should fail (as \[Can Drive] only checks if the person is \> 18\). Then amend \[Can Drive] to pass by checking both conditions. Small failing test, then write some of the measure, pass. Repeat.

# DAX Tests Query Structure

### Example:

DEFINE    VAR Age10 \= CALCULATE(        \[Invoice Age],        'Invoices'\[ID] \= "0,1",        'Age From'\[Age From] \= "Due Date",        'Dates'\[Date] \<\= DATE(2023, 2, 11)    )    VAR Age27 \= CALCULATE(        \[Invoice Age],        'Invoices'\[ID] \= "0,1",        'Age From'\[Age From] \= "Due Date",        'Financial Periods'\[Year Beginning] \= "Jan 23",        'Financial Periods'\[Period Number] \= 2    )  
    VAR Tests \= UNION(        \-\- Invoice Age tests        ROW(            "Test Name", "Invoice due 1 Feb is 10 days old on 11 Feb",            "Expected Value", 10,            "Actual Value", Age10        ),        ROW(            "Test Name", "Invoice due 1 Feb is 27 days old on perod end Feb",            "Expected Value", 27,            "Actual Value", Age27        )  
    )  
    VAR TestsWithResult \= ADDCOLUMNS(        Tests,        "Test Pass", IF( \[Expected Value] \= \[Actual Value], "True", "False" )    )    VAR TestSummary \= ROW(        "Tests Passed", COUNTROWS(FILTER(                TestsWithResult,                \[Test Pass] \= TRUE()            )),        "Tests Failed", COUNTROWS(FILTER(                TestsWithResult,                \[Test Pass] \= FALSE()            ))    )  
EVALUATE    TestSummary  
  
EVALUATE    TestsWithResult
  
### Output TestWithResult:

### DAX Tests Output.png

  


# Test Data

  


### Test Database SQL Script:

Example of test database SQL script made exclusively for Credit Control Dashboard.  


\-\- DO NOT AMEND THE TEST DATA OF PREVIOUS TESTS! \-\- USE \[master];  
ALTERDATABASE CreditControlTestSET    single\_userWITH    ROLLBACK IMMEDIATE;  
GO\-\-DROPDATABASE IF EXISTS CreditControlTest;  
GO\-\- CREATEDATABASE CreditControlTest;  
GO\-\- USE CreditControlTest;  
CREATEUSER \[NT Service\\Codis BI] FORLOGIN \[NT Service\\Codis BI];  
EXEC sp\_addrolemember 'db\_datareader',\[NT Service\\Codis BI];  
CREATE TABLE    SLAllocationHeader (        SLAllocationHeaderID bigint NULL,        SLAllocationTypeID bigint NULL DEFAULT 0,        UserName NVARCHAR(MAX) DEFAULT 'John',        AllocationDate datetime NULL,        IsComplete INT DEFAULT 1    );  
CREATE TABLE    SLAllocationType (        SLAllocationTypeID bigint NULL,        \[Name] VARCHAR(30) NULL    );  
CREATE TABLE    SLAllocationTran (        SLAllocationTranID bigint NULL,        SLAllocationHeaderID bigint NULL,        SLPostedCustomerTranID bigint NULL,        AllocationValue DECIMAL(18, 2) NULL    );  
CREATE TABLE    SLCustomerAccount (        SLCustomerAccountID bigint NULL,        CustomerAccountNumber VARCHAR(8) NULL,        CustomerAccountName VARCHAR(60) NULL,        CustomerAccountShortName VARCHAR(8) NULL,        AccountBalance DECIMAL(18, 2) NULL,        CreditLimit DECIMAL(18, 2) NULL,        PaymentTermsInDays SMALLINT NULL,        SYSPaymentTermsBasisID bigint NULL,        SYSAccountStatusID bigint NULL    );  
CREATE TABLE    SLPostedCustomerTran (        SLPostedCustomerTranID bigint NULL,        SLCustomerAccountID bigint NULL,        TransactionDate datetime NULL,        TransactionReference VARCHAR(20) NULL,        SecondReference VARCHAR(20) NULL,        GoodsValueInAccountCurrency DECIMAL(18, 2) NULL,        AllocatedValue DECIMAL(18, 2) NULL,        DueDate datetime NULL,        FullSettlementDate datetime NULL,        DocumentToBaseCurrencyRate DECIMAL(18, 6) NULL DEFAULT 1,        UniqueReferenceNumber bigint NULL,        UserName VARCHAR(20) NULL,        QueryCode VARCHAR(20) NULL,        SYSTraderTranTypeID bigint NULL    );  
CREATE TABLE    SLRevalAllocationTran (        SYSTraderRevalAllocTypeID bigint NULL,        SLPostedCustomerTranID bigint NULL,        EntryDate datetime NULL,        DocumentToBaseCurrencyRate DECIMAL(18, 6) NULL    );  
CREATE TABLE    SYSAccountingPeriod (        SYSAccountingPeriodID bigint NULL,        SYSFinancialYearID bigint NULL,        PeriodNumber SMALLINT NULL,        StartDate datetime NULL,        EndDate datetime NULL    );  
CREATE TABLE    SYSAccountStatus (        SYSAccountStatusID bigint NULL,        Name VARCHAR(20) NULL    );  
CREATE TABLE    SYSAgeingPeriod (        SYSAgeingPeriodID bigint NULL,        DaysPeriodStartsAfter SMALLINT NULL,        SalesLedgerOrPurchaseLedger BIT NULL    );  
CREATE TABLE    SYSFinancialYear (        SYSFinancialYearID bigint NULL,        FinancialYearStartDate datetime NULL,        YearRelativeToCurrentYear INT NULL    );  
CREATE TABLE    SYSPaymentTermsBasis (        SYSPaymentTermsBasisID bigint NULL,        Name VARCHAR(50) NULL    );  
INSERT INTO    SLPostedCustomerTran (        SLPostedCustomerTranID,        SLCustomerAccountID,        TransactionDate,        DueDate,        FullSettlementDate,        SYSTraderTranTypeID,        GoodsValueInAccountCurrency,        AllocatedValue    )VALUES    \-\- 2 invoices which took a long time to pay    (        1,        101,        '2023\-01\-01',        '2023\-02\-01',        '2023\-10\-10',        4,        1000,        1000    ),    (        2,        102,        '2023\-02\-01',        '2023\-03\-01',        '2023\-10\-10',        4,        2000,        2000    ),    \-\- an invoice which was paid in 7 days    (        3,        102,        '2023\-02\-01',        '2023\-03\-01',        '2023\-02\-08',        4,        300,        300    ),    \-\- an Unsettled Invoice    (4, 102, '2023\-03\-01', '2023\-04\-01', NULL, 4, 400, 0),    \-\- an invoice for which a Credit note was issued    (5, 102, '2023\-02\-20', '2023\-03\-20', NULL, 4, 750, 750),    (        6,        102,        '2023\-08\-01',        '2023\-08\-01',        NULL,        5,        \-750,        \-750    ),    \-\- Credit note that has been partially paid    (        7,        102,        '2023\-03\-01',        '2023\-03\-01',        NULL,        5,        \-1000,        \-300    );  
INSERT INTO    SLAllocationHeader (SLAllocationHeaderID, AllocationDate)VALUES    \-\- receipts for the 2 long standing invoices    (1, '2023\-02\-10'),    (2, '2023\-03\-10'),    (3, '2023\-04\-10'),    (4, '2023\-05\-10'),    (5, '2023\-10\-10'),    \-\- receipt for the quick paid invoice    (6, '2023\-02\-08'),    \-\- Matching the credit note to invoice    (7, '2023\-08\-01'),    \-\- partially paying the credit note    (8, '2023\-03\-01');  
INSERT INTO    SLAllocationTran (        SLAllocationTranID,        SLAllocationHeaderID,        SLPostedCustomerTranID,        AllocationValue    )VALUES    \-\- allocations for the long standing invoices    (1, 1, 1, 100),    (2, 1, 2, 100),    (3, 2, 1, 100),    (4, 2, 2, 100),    (5, 3, 1, 100),    (6, 3, 2, 100),    (7, 4, 1, 100),    (8, 4, 2, 100),    (9, 5, 1, 600),    (10, 5, 2, 1600),    \-\- allocation for the quick paid invoice    (11, 6, 3, 300),    \-\- allocation for Invoice having credit note issued    (12, 7, 5, 750),    (13, 7, 6, \-750),    (14, 8, 7, \-300);  
INSERT INTO    SYSAccountingPeriod (        SYSFinancialYearID,        SYSAccountingPeriodID,        PeriodNumber,        StartDate,        EndDate    )VALUES    (1, 1, 1, '2023\-01\-01', '2023\-01\-31'),    (1, 2, 2, '2023\-02\-01', '2023\-02\-28'),    (1, 3, 3, '2023\-03\-01', '2023\-03\-31'),    (1, 4, 4, '2023\-04\-01', '2023\-04\-30'),    (1, 5, 5, '2023\-05\-01', '2023\-05\-31'),    (1, 6, 6, '2023\-06\-01', '2023\-06\-30'),    (1, 7, 7, '2023\-07\-01', '2023\-07\-31'),    (1, 8, 8, '2023\-08\-01', '2023\-08\-31'),    (1, 9, 9, '2023\-09\-01', '2023\-09\-30'),    (1, 10, 10, '2023\-10\-01', '2023\-10\-31'),    (1, 11, 11, '2023\-11\-01', '2023\-11\-30'),    (1, 12, 12, '2023\-12\-01', '2023\-12\-31');  
INSERT INTO    SYSFinancialYear (        SYSFinancialYearID,        FinancialYearStartDate,        YearRelativeToCurrentYear    )VALUES    (1, '2023\-01\-01', 0);  
INSERT INTO    SYSAgeingPeriod (        SYSAgeingPeriodID,        SalesLedgerOrPurchaseLedger,        DaysPeriodStartsAfter    )VALUES    (1, 0, 30),    (2, 0, 60),    (3, 0, 90),    (4, 0, 120);  
INSERT INTO    SLAllocationType (SLAllocationTypeID, Name)VALUES    (0, N'Manual Receipt'),    (1, N'Write Off'),    (2, N'Reverse Posting'),    (3, N'Automatic Allocation'),    (4, N'Small Values Write Off'),    (5, N'Contra Entry'),    (6, N'Free Text Invoice'),    (7, N'Reverse Finance Charge'),    (8, N'Manual Notification'),    (9, N'Manual Opening Balance'),    (10, N'Manual Payment');  
INSERT INTO    SLCustomerAccount (        SLCustomerAccountID,        CustomerAccountNumber,        CustomerAccountName,        CustomerAccountShortName    )VALUES    (101, 1001, 'Thomas Edison', 'Thomas'),    (102, 1002, 'Kapil Sharma', 'Kapil');  
  


###
