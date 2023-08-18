---
title: "OLE Automation Result Sets"
description: Learn that if an OLE Automation property or method returns data in an array with one or two dimensions, the array is returned to the client as a result set.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/10/2022"
ms.service: sql
ms.subservice: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
  - "data types [SQL Server], OLE Automation"
  - "two-dimensional arrays"
  - "one-dimensional arrays"
  - "result sets [SQL Server], OLE Automation"
  - "OLE Automation [SQL Server], result sets"
  - "arrays [SQL Server]"
monikerRange: ">=sql-server-2016"
---
# OLE Automation Result Sets
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  If an OLE Automation property or method returns data in an array with one or two dimensions, the array is returned to the client as a result set:  
  
-   A one-dimensional array is returned to the client as a single-row result set with as many columns as there are elements in the array. For example, an array(10) is returned as a single row of 10 columns.  
  
-   A two-dimensional array is returned to the client as a result set with as many columns as there are elements in the first dimension of the array and with as many rows as there are elements in the second dimension of the array. For example, an array(2,3) is returned as 2 columns in 3 rows.  
  
 When a property return value or method return value is an array, `sp_OAGetProperty` or `sp_OAMethod` returns a result set to the client. (Method output parameters cannot be arrays.) These procedures scan all the data values in the array to determine the appropriate [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data types and data lengths to use for each column in the result set. For a particular column, these procedures use the data type and length required to represent all data values in that column.  
  
 When all data values in a column share the same data type, that data type is used for the whole column. When data values in a column are different data types, the data type of the whole column is chosen based on the following table. To use the following table, find one data type along the left row axis and a second data type along the top column axis. The intersection of the row and column describes the data type of the result set column.  
  
|   | **int** | **float** | **money** | **datetime** | **varchar** | **nvarchar** |
| - | ------- | --------- | --------- | ------------ | ----------- | ------------ |
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## See also

- [Ole Automation Procedures Server Configuration Option](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  

## Next steps

- [OLE Automation Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
