---
title: Excelerator on Oracle
tags:
- Consultancy
description: 'Symptom(s): Oracle* will not install EngineStart.exe error Error: EngineStart.exe
  has generated errors and will be closed by Windows*. You will need…'
created: '2017-08-30'
modified: '2017-08-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20on%20Oracle.aspx
---

- **Symptom(s):**  
 Oracle\* will not install
- EngineStart.exe error
- Error: EngineStart.exe has generated errors and will be closed by Windows\*. You will need to restart the program.  
  
**Cause:**  
 The Just\-In\-Time.dll driver may not properly recognize the Intel® Pentium® 4 processor, and may generate an error when executed on the Pentium 4 processor platform.  
  
**Solution:**  
 Intel has identified that applications which use the Symantec Just\-In\-Time\* Compiler library file ("symcjit.dll" for Microsoft Windows\* operating system and "symc\_jlt.nlm" for Novell NetWare\* 5\.1\) may not run properly on Pentium® 4 processor systems because the library does not properly identify the processor.  
 The failure typically is that the affected application such as Oracle 8i, simply terminates. Under Microsoft Windows\*, the properties of the DLL are: "Symantec Java! Just\-In\-Time Compiler Version 3\.10\.107 for JDK 1\.2 Copyright (C) 1996\-99 Symantec Corporation Dynamic Link Library file". DLLs older than this will also not work. To confirm the version you are using, select the DLL, right click on the selected DLL and select Properties, and then the Version tab. Intel encourages all Software developers to do the following immediately:   
Check if your application(s) uses the Symantec Just\-In\-Time Library file   
Request an updated library file from your provider   
Test your application with the new library file on PentiumÂ® 4 processor system   
Ensure you have plans in place to provide application updates and address customer concerns   
\*Other brands and names are property of their respective owners  
 If you are installing into Windows\* 2000, one workaround recommendation by Oracle for this problem is:  
 Install the latest Windows\* 2000 Service Pack patch: <http://www.microsoft.com/windows2000/downloads/>   
Create a temporary directory on your Intel PentiumÂ® 4 processor server (e.g. \\TEMP).   
Copy the contents of the Oracle\* Server CD to the temporary directory created in step 2\.   
Search the directory structure created in step 2 for the existence of the filename SYMCJIT.DLL.   
Rename each copy of the SYMCJIT.DLL to SYMCJIT.OLD.   
Run the SETUP.EXE from the \\TEMP\\install\\win32 directory and install Oracle 8\.1\.x.   
If you have any other questions on this work around, please contact Oracle.  
  
   
  
HKEY\_LOCAL\_MACHINE\\SOFTWARE\\ORACLE\\OLEDB  
  
Fetchsize \- defaults to 100\.  Set higher e.g. 300  
  
   
  
Root)OraHOme91  
  
            (a)Oracle Programmer  
  
            (b)Development Tools  
  
                        1\)Oracle Object For OLE  
  
                        2\)Oracle ODBC Driver  
  
                                    (i)3\)Oracle NET CLient Manager  
  
                        3\)Oracle OLEDB Provider
