---
title: "SQLXML Is Not Installed in SQL Server"
description: SQLXML Is Not Installed in SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/14/2017"
ms.service: sql
ms.topic: "reference"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# SQLXML Is Not Installed in SQL Server
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  Before [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)], SQLXML 4.0 was released with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and was part of the default installation of all [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versions except for [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Starting with [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)], the latest version of SQLXML (SQLXML 4.0 SP1) is no longer included in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. To install SQLXML 4.0 SP1, download it from [Install Location for SQLXML 4.0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 If an application runs on [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and requires SQLXML 4.0, you have to download and install SQLXML 4.0 SP1.  
  
## SQLXML 4.0 SP1 Behavior with New Data Types Using SQLOLEDB and SQL Server Native Client OLE DB Provider  
 [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] introduced the following data types, which developers using SQLXML might want to use:  
  
-   **Date**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 When using SQLXML 4.0 SP1 with either SQLOLEDB or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB from [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], these types appear as strings to a developer. SQLXML 4.0 SP1 will enable these four new data types as built-in scalar types when used with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 or later. Until you download SQLXML 4.0 SP1, mapping these types to non-string types might cause truncation of some data. For example, mapping **DateTime2** to **xsd:date** will cause data to be truncated to the [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** precision of 3.33 milliseconds.  
  
## See Also  
 [SQLXML 4.0 Programming Concepts](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
