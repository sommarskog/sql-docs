---
title: "Fetch single row with IRow (OLE DB driver)"
description: IRow allows direct access to columns of a single row object. The IRow interface in the OLE DB Driver for SQL Server is simplified to increase performance.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "fetching rows"
  - "IRow interface"
  - "single row fetching [OLE DB Driver for SQL Server]"
  - "OLE DB rowsets, fetching"
  - "rowsets [OLE DB], fetching"
  - "OLE DB Driver for SQL Server, fetching"
---
# Fetching a Single Row with IRow (OLE DB Driver)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  The **IRow** interface implementation in the OLE DB Driver for SQL Server is simplified to increase performance. **IRow** allows direct access to columns of a single row object. If you know beforehand that the result of a command execution will produce exactly one row, **IRow** will retrieve the columns of that row. If the result set includes multiple rows, **IRow** will expose only the first row.  
  
 The **IRow** implementation does not allow any navigation of the row. Each column in the row is accessed only one time with one exception: A column can be accessed one time to find the column size and again to fetch the data.  
  
> [!NOTE]  
>  **IRow::Open** supports only DBGUID_STREAM and DBGUID_NULL type of objects to be opened.  
  
 To obtain a row object using **ICommand::Execute** method, IID_IRow must be passed. The **IMultipleResults** interface must be used to handle multiple result sets. **IMultipleResults** supports **IRow** and **IRowset**. **IRowset** is used for bulk operations.  
  
## In This Section  
  
-   [Using IRow::GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## See Also  
 [Rowsets](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
