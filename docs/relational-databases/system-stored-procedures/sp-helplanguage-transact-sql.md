---
title: "sp_helplanguage (Transact-SQL)"
description: "sp_helplanguage (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_helplanguage"
  - "sp_helplanguage_TSQL"
helpviewer_keywords:
  - "sp_helplanguage"
  - "default languages"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sp_helplanguage (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Reports information about a particular alternative language or about all languages in [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)].  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## Arguments  
`[ @language = ] 'language'`
 Is the name of the alternative language for which to display information. *language* is **sysname**, with a default of NULL. If *language* is specified, information about the specified language is returned. If language is not specified, information about all languages in the **sys.syslanguages** compatibility view is returned.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|Language identification number.|  
|**dateformat**|**nchar(3)**|Format of the date.|  
|**datefirst**|**tinyint**|First day of the week: 1 for Monday, 2 for Tuesday, and so on through 7 for Sunday.|  
|**upgrade**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] version of the last upgrade for this language.|  
|**name**|**sysname**|Language name.|  
|**alias**|**sysname**|Alternative name of the language.|  
|**months**|**nvarchar(372)**|Month names.|  
|**shortmonths**|**nvarchar(132)**|Short month names.|  
|**days**|**nvarchar(217)**|Day names.|  
|**lcid**|**int**|Windows locale ID for the language.|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] message group ID.|  
  
## Permissions  
 Requires membership in the **public** role.  
  
## Examples  
  
### A. Returning information about a single language  
 The following example displays information about the alternative language `French`.  
  
```  
sp_helplanguage French;  
```  
  
### B. Returning information about all languages  
 The following example displays information about all installed alternative languages.  
  
```  
sp_helplanguage;  
```  
  
## See Also  
 [Database Engine Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
