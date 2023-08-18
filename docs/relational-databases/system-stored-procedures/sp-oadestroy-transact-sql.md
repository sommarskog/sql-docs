---
title: "sp_OADestroy (Transact-SQL)"
description: "sp_OADestroy (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_OADestroy_TSQL"
  - "sp_OADestroy"
helpviewer_keywords:
  - "sp_OADestroy"
dev_langs:
  - "TSQL"
---
# sp_OADestroy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Destroys a created OLE object.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## Arguments  
 *objecttoken*  
 Is the object token of an OLE object that was previously created by using **sp_OACreate**.  
  
## Return Code Values  
 0 (success) or a nonzero number (failure) that is the integer value of the HRESULT returned by the OLE Automation object.  
  
 For more information about HRESULT Return Codes, see [OLE Automation Return Codes and Error Information](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## Remarks  
 If **sp_OADestroy** is not called, the created OLE object is automatically destroyed at the end of the batch.  
  
## Permissions  
 Requires membership in the **sysadmin** fixed server role or execute permission directly on this Stored Procedure. `Ole Automation Procedures` configuration must be **enabled** to use any system procedure related to OLE Automation.  
  
## Examples  
 The following example destroys the previously created **SQLServer** object.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## See Also  
 [OLE Automation Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation Sample Script](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
