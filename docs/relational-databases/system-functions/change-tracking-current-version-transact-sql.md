---
title: "CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)"
description: "CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "08/08/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "CHANGE_TRACKING_CURRENT_VERSION_TSQL"
  - "CHANGE_TRACKING_CURRENT_VERSION"
helpviewer_keywords:
  - "change tracking [SQL Server], CHANGE_TRACKING_CURRENT_VERSION"
  - "CHANGE_TRACKING_CURRENT_VERSION"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns a version that is associated with the last committed transaction. This version can be used when you enumerate changes by using [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
CHANGE_TRACKING_CURRENT_VERSION ( )  
```  
  
## Return Type  
 **bigint**  
  
## Remarks  
 Returns NULL when change tracking is not enabled for the database.  
  
## Examples  
 The following example declares the local variable `@next_baseline` for storing the current version of tracked changes, and then uses the `CHANGE_TRACKING_CURRENT_VERSION()` function to obtain the value for the variable.  
  
```sql  
DECLARE @next_baseline bigint;  
SET @next_baseline = CHANGE_TRACKING_CURRENT_VERSION();  
```  
  
## See Also  
 [Change Tracking Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Track Data Changes &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
