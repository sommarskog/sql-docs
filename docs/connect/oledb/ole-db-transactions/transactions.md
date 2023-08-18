---
title: Transactions (OLE DB driver)
description: Learn how the OLE DB Driver for SQL Server supports local transactions. Use the Microsoft Distributed Transaction Coordinator for distributed transactions.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "OLE DB, transactions"
  - "transactions [OLE DB]"
  - "OLE DB Driver for SQL Server, transactions"
---
# Transactions
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  The OLE DB Driver for SQL Server implements local transaction support. The consumer can use distributed or coordinated transactions by using Microsoft Distributed Transaction Coordinator (MS DTC). For consumers requiring transaction control that spans multiple sessions, the OLE DB Driver for SQL Server can join transactions initiated and maintained by MS DTC.  
  
 By default, the OLE DB Driver for SQL Server uses an autocommit transaction mode, where each discrete action on a consumer session comprises a complete transaction against an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. The OLE DB Driver for SQL Server autocommit mode is local, and autocommit transactions never span more than a single session.  
  
 The OLE DB Driver for SQL Server exposes the **ITransactionLocal** interface, allowing the consumer to use explicitly and implicitly start transactions on a single connection to an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. The OLE DB Driver for SQL Server does not support nested local transactions.  
  
## In This Section  
  
-   [Supporting Local Transactions](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Supporting Distributed Transactions](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Isolation Levels &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## See Also  
 [OLE DB Driver for SQL Server Programming](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
