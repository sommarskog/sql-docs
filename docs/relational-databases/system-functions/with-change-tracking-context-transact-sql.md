---
title: "WITH CHANGE_TRACKING_CONTEXT (Transact-SQL)"
description: "WITH CHANGE_TRACKING_CONTEXT (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "08/08/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "WITH_CHANGE_TRACKING_CONTEXT_TSQL"
  - "WITH CHANGE_TRACKING_CONTEXT"
helpviewer_keywords:
  - "WITH CHANGE_TRACKING_CONTEXT"
  - "change tracking [SQL Server], WITH CHANGE_TRACKING_CONTEXT"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# WITH CHANGE_TRACKING_CONTEXT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Enables the context of a change to be specified, such as an originator ID, when data is changed. For example, when using change tracking, an application might want to differentiate between changes that were made by the application itself and changes that were made to the data outside the application.  

 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
#### Parameters  
 *context*  
 Is the contextual information that is supplied by the calling application and stored with the change tracking information for the change. *context* is **varbinary(128)**.  
  
 The value can be a constant or a variable, but cannot be NULL.  
  
## Examples  
 The following example sets the change tracking context for a data change.  
  
```  
WITH CHANGE_TRACKING_CONTEXT ( context )  
```  
  
## See Also  
 [Change Tracking Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Track Data Changes &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
