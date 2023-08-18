---
title: "sp_dbcmptlevel (Transact-SQL)"
description: "sp_dbcmptlevel (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_dbcmptlevel"
  - "sp_dbcmptlevel_TSQL"
helpviewer_keywords:
  - "sp_dbcmptlevel"
dev_langs:
  - "TSQL"
---
# sp_dbcmptlevel (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sets certain database behaviors to be compatible with the specified version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)instead.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## Arguments  
`[ @dbname = ] name`
 Is the name of the database for which the compatibility level is to be changed. Database names must conform to the rules for identifiers. *name* is **sysname**, with a default of NULL.  
  
`[ @new_cmptlevel = ] version`
 Is the version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] with which the database is to be made compatible. *version* is **tinyint**, with a default of NULL. The value must be one of the following:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
 If no parameters are specified or if the *name* parameter is not specified, **sp_dbcmptlevel** returns an error.  
  
 If *name* is specified without *version*, the [!INCLUDE[ssDE](../../includes/ssde-md.md)] returns a message displaying the current compatibility level of the specified database.  
  
## Remarks  
 For a description of compatibilities levels, see [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## Permissions  
 Only the database owner, members of the **sysadmin** fixed server role, and the **db_owner** fixed database role (if you are changing the current database) can execute this procedure.  
  
## See Also  
 [Database Engine Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Reserved Keywords &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
