---
title: "sys.fn_cdc_get_max_lsn (Transact-SQL)"
description: "sys.fn_cdc_get_max_lsn (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.fn_cdc_get_max_lsn"
  - "fn_cdc_get_max_lsn"
  - "fn_cdc_get_max_lsn_TSQL"
  - "sys.fn_cdc_get_max_lsn_TSQL"
helpviewer_keywords:
  - "fn_cdc_get_max_lsn"
  - "sys.fn_cdc_get_max_lsn"
dev_langs:
  - "TSQL"
---
# sys.fn_cdc_get_max_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns the maximum log sequence number (LSN) from the start_lsn column in the [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) system table. You can use this function to return the high endpoint of the change data capture timeline for any capture instance.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## Return Types  
 **binary(10)**  
  
## Remarks  
 This function returns the maximum LSN in the start_lsn column of the [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) table. As such, it is the last LSN processed by the capture process when changes are propagated to the database change tables. It serves as the high endpoint for the all timelines that are associated with capture instances defined for the database.  
  
 The function is typically used to obtain an appropriate high endpoint for a query interval.  
  
## Permissions  
 Requires membership in the public database role.  
  
## Examples  
  
### A. Returning the maximum LSN value  
 The following example returns the maximum LSN for all capture instances in the [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database.  
  
```  
USE AdventureWorks2022;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### B. Setting the high endpoint of a query range  
 The following example uses the maximum LSN returned by `sys.fn_cdc_get_max_lsn` to set the high endpoint for a query range for the capture instance `HumanResources_Employee`.  
  
```  
USE AdventureWorks2022;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## See Also  
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [The Transaction Log &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
