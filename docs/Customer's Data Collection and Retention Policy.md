---
title: Customer's Data Collection and Retention Policy
tags:
- IT
- Security
description: 1. Purpose This policy tells Codis staff how to handle customer data
  safely and legally — particularly when accessing customer systems for support…
created: '2023-08-09'
modified: '2026-04-21'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Customer's%20Data%20Collection%20and%20Retention%20Policy.aspx
---

## 1\. Purpose

This policy tells Codis staff how to handle customer data safely and legally — particularly when accessing customer systems for support work. It exists to ensure Codis meets its obligations as a Data Processor under its Data Processing Agreements with customers.  

## 2\. Who This Applies To

All Codis staff, including remote support staff working from outside the UK.  

## 3\. The Golden Rules

1. **Only collect data you actually need** for the support task at hand.
2. **Delete customer data as soon as the task is complete.** Do not hold on to it "just in case."
3. **Customer data must only ever be stored on your Codis\-assigned UK PC** (the Azure\-hosted machine). Never copy it to your personal PC or any personal storage (including personal cloud drives, USB sticks, or email).
4. **Never transfer customer data outside the UK** unless a customer has explicitly agreed to this in writing.
5. **Keep customer data confidential.** Do not share it with anyone who doesn't need it for the task.

## 4\. Copying Data from Customers' sites

Follow the procedure [here](How to Copy Data from Customers' Sites.md).  

## 5\. SQL Backups

This section specifically covers taking SQL backups of customer Sage 200 systems, which is a common support task.

**Step 1 — Before you start**

- Confirm there is a legitimate support reason to take a backup.
- You must be connected to the customer's server via your Codis\-assigned UK PC (the Azure machine). Do not log in from your personal PC.

**Step 2 — Taking the backup**

- Log into the customer's server using only your Codis\-provided credentials.
- Take the SQL backup as required for the support task.

**Step 3 — Copying the backup**

- Use the procedure documented [here](How to Copy Data from Customers' Sites.md).
- **Do not copy the backup to your personal PC in India or any other personal device.**

**Step 4 — Using the backup**

- Use the backup only for the purpose of diagnosing or resolving the customer's issue.

**Step 5 — Deleting the backup**

- Once the task is complete, delete the backup file from your Codis UK PC.
- Do not retain it beyond the point it is needed.

## 6\. Remote Working — Which PC to Use

| Task | Allowed PC |
| --- | --- |
| Logging into a customer server | Codis UK PC (Azure) only |
| Storing a customer SQL backup | Codis UK PC (Azure) only |
| Running tests against customer data | Codis UK PC (Azure) only |
| Personal work / non\-customer tasks | Personal PC |

Your personal PC must **never** hold customer data.

## 7\. Data Breaches — What to Do

If you accidentally copy customer data to a personal device, share it with the wrong person, lose access to it, or suspect it has been accessed by someone unauthorised:

- **Report it to your manager immediately** — do not wait.
- Codis is required to notify customers within 48 hours of becoming aware of a breach. Your prompt reporting makes this possible.
- Do not attempt to quietly fix the problem without telling anyone.

## 8\. Frequently Asked Questions

**Can I just quickly copy the backup to my personal PC to run a test?**

No. Even temporarily, customer data must not be held on personal devices.

**What if the Azure PC is too slow or unavailable?**

Contact your manager. The answer is still no — do not use your personal PC as a workaround.

**How long can I keep a backup?**

Only as long as it takes to complete the support task. Delete it immediately afterwards.

**What counts as "customer data"?**

Any data from a customer's system — including SQL backups, exported files, screenshots containing customer records, or any data copied out of Sage 200\.

**What if a customer asks me to keep a backup for future use?**

Escalate this to your manager. This would require explicit written agreement and is not standard practice.  

## 9\. Acknowledgement

All staff must confirm they have read and understood this policy. By continuing in your role at Codis, you agree to follow these rules. Breaches of this policy may result in disciplinary action.
