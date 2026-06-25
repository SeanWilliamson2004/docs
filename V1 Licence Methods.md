---
title: V1 Licence Methods
tags: []
description: 'Case "A": LicenseAlgorithm = COMPNO_MACADDR '' MAC address Case "B":
  LicenseAlgorithm = COMPNO_BIOS + COMPNO_HDSERIAL '' Bios + hdserial Case "C":…'
created: '2024-02-23'
modified: '2024-02-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/V1%20Licence%20Methods.aspx
---

Case "A": LicenseAlgorithm \= COMPNO\_MACADDR        ' MAC address        Case "B": LicenseAlgorithm \= COMPNO\_BIOS \+ COMPNO\_HDSERIAL      ' Bios \+ hdserial        Case "C": LicenseAlgorithm \= COMPNO\_FILESTART       ' filestart        Case "D": LicenseAlgorithm \= COMPNO\_ENHANCED  
  
https://www.softwarekey.com/help/plusman/Content/Concepts/Concepts\_Computer\_ID\_Number.htm  
  


| ID TYPE | \# | DESCRIPTION |
| --- | --- | --- |
| COMPNO\_BIOS | 1 | No longer supported. |
| COMPNO\_HDSERIAL | 2 | Identifies the drive volume serial number of the specified drive. A drive letter must be specified, or a value of "0" may be specified to use the drive upon which Windows is installed. |
| COMPNO\_HDLOCK | 4 | No longer supported. |
| COMPNO\_HDTYPE | 8 | No longer supported. |
| COMPNO\_NETNAME | 16 | Calculates number based upon network server profile by determining the network server name and volume for a given drive letter or UNC path. |
| COMPNO\_MACADDR | 32 | Deprecated.  SW \- I think that this used the MAC address of the network card. |
| COMPNO\_FILESTART | 64 | Deprecated. |
| COMPNO\_WINPRODID | 128 | Uses Windows ProductID and ProductKey created when Windows is installed. |
| COMPNO\_IPADDR | 256 | Calculates a number based upon the TCP/IP address of a given server name, drive letter connected to a network server, or UNC path to a server. |
| COMPNO\_ENHANCED | 65536 | Uses the [Enhanced Computer ID Algorithms](https://www.softwarekey.com/help/plusman/Content/Concepts/Enhanced_Computer_ID_Algorithms.htm) |
| COMPNO\_SERVER\_MACADDR | 131072 | Provide a server's UNC path, host name, or IP address through either the filename or the hard drive parameter (you may leave one as an empty string) and this will compute a number based on that server's MAC address. Please be considerate of the possibility of redundant Network Interface Cards (NIC) when using this algorithm (you may need to authorize the server once for each NIC). |

  
  
https://www.softwarekey.com/help/plusman/Content/Concepts/Enhanced\_Computer\_ID\_Algor  
  


| COMPNO\_MACADDR | 32 | Calculates a number based upon the Ethernet (MAC) address of an installed Ethernet LAN adapter. |
| --- | --- | --- |
| COMPNO\_FILESTART | 64 | Identifies the starting location of a non\-movable file. It is very unlikely for two computers to store the same file in the same location. A path and filename must be specified. |

  
At some point Seema said this:  
  


Licence Method A: PC’s and Servers

Licence Method B: Old Laptop – we used to use this but now don’t unless there is no option D available

Licence Method C: Used if PC/Laptop keeps changing the Computer ID and losing the licence (more common on Laptops)

Licence Method D: Laptops
