---
title: Connecting 2 hyper to redirect SQL db connection
tags: []
description: '🔹 Step 1: Check/Setup Networking in Hyper-V Open Hyper-V Manager on
  your host. On the right-hand side, click Virtual Switch Manager . Create a new…'
created: '2025-10-13'
modified: '2025-10-13'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Connecting%202%20hyper%20to%20redirect%20SQL%20connection.aspx
---

## 🔹 Step 1: Check/Setup Networking in Hyper\-V

1. Open **Hyper\-V Manager** on your host.
2. On the right\-hand side, click **Virtual Switch Manager**.
3. Create a **new switch** (choose one depending on your need):
	- **External** → VMs get IP from your physical LAN (they’ll be like real PCs on your network).
	- **Internal** → VMs can talk to each other \+ host, but not to outside internet.
	- **Private** → VMs talk only to each other (no host, no internet).  

	👉 I recommend **Internal** if you just want VM1 ↔ VM2 communication.
4. Assign this switch to **both VM1 and VM2**:
	- Right\-click VM → **Settings** → **Network Adapter** → pick the switch you created.

---

## 🔹 Step 2: Verify Connectivity

1. Start both VMs.
2. Inside **VM1**, run:

      ipconfig  
      Note down its IP address.1. Inside **VM2**, try:
	- If it replies, networking is fine.
	- If not, check firewall or switch settings.

---

## 🔹 Step 3: Enable SQL Remote Access (on VM1\)

1. Open **SQL Server Configuration Manager** inside VM1\.
2. Under **SQL Server Network Configuration → Protocols for MSSQLSERVER**, enable **TCP/IP**.
3. Right\-click **TCP/IP → Properties → IP Addresses**:
	- Scroll to the bottom, make sure **TCP Port \= 1433** (default).
	- Apply and restart the SQL Server service.

---

## 🔹 Step 4: Firewall Rule on VM1

1. Open **Windows Defender Firewall → Advanced Settings**.
2. Add **Inbound Rule** → Port → TCP → 1433 → Allow.

---

## 🔹 Step 5: Connect from VM2

On VM2, open SQL Server Management Studio (SSMS) or any client and connect to:

```
Server name: <VM1_IP>,1433Authentication: SQL Authentication or Windows Authentication (if domain/trusted setup)
```

---

✅ After this, VM2 will be able to query the SQL instance running on VM1\.

```
ping <VM1_IP>
```

```
ipconfig 
```

```
  

```

```
Note: Step 5 is not required if we are testing Sage 1000 Excelerator, we can add details in connection.  
```

```
  

```

```
  

```
