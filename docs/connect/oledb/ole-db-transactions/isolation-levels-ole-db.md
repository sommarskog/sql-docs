---
title: "Isolation levels (OLE DB driver)"
description: Learn how an OLE DB Driver for SQL Server consumer can control the transaction-isolation level for a connection.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "OLE DB, transactions"
  - "isolation levels [OLE DB]"
  - "transactions [OLE DB]"
  - "OLE DB Driver for SQL Server, transactions"
---
# Isolation Levels (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clients can control transaction-isolation levels for a connection. To control transaction-isolation level, the OLE DB Driver for SQL Server consumer uses:  
  
-   DBPROPSET_SESSION property DBPROP_SESS_AUTOCOMMITISOLEVELS for the OLE DB Driver for SQL Server default autocommit mode.  
  
     The OLE DB Driver for SQL Server default for the level is DBPROPVAL_TI_READCOMMITTED.  
  
-   The *isoLevel* parameter of the **ITransactionLocal::StartTransaction** method for local manual-commit transactions.  
  
-   The *isoLevel* parameter of the **ITransactionDispenser::BeginTransaction** method for MS DTC-coordinated distributed transactions.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] allows read-only access at the dirty read isolation level. All other levels restrict concurrency by applying locks to [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objects. As the client requires greater concurrency levels, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applies greater restrictions on concurrent access to data. To maintain the highest level of concurrent access to data, the OLE DB Driver for SQL Server consumer should intelligently control its requests for specific concurrency levels.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduced snapshot isolation level. For more information, see [Working with Snapshot Isolation](../../oledb/features/working-with-snapshot-isolation.md).  
  
## See Also  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)  
  
  
