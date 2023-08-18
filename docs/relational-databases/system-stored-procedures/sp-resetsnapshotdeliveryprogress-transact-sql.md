---
title: "sp_resetsnapshotdeliveryprogress (Transact-SQL)"
description: "sp_resetsnapshotdeliveryprogress (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_resetsnapshotdeliveryprogress"
  - "sp_resetsnapshotdeliveryprogress_TSQL"
helpviewer_keywords:
  - "sp_resetsnapshotdeliveryprogress"
dev_langs:
  - "TSQL"
---
# sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Resets the snapshot delivery process for a pull subscription so that snapshot delivery can be restarted. Executed at the Subscriber on the subscription database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## Arguments  
`[ @verbose_level = ] verbose_level`
 Specifies the amount of information returned. *verbose_level*is **int**, with a default of **1**. A value of **1** means that an error is returned if the necessary locks cannot be obtained on the **MSsnapshotdeliveryprogress** table, and **0** means that no error is returned.  
  
`[ @drop_table = ] 'drop_table'`
 Is whether to drop or truncate the table containing information on the progress of the snapshot.*drop_table* is **nvarchar(5)**, with a default of **FALSE**. false means that the table is truncated, and true means the table is dropped.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_resetsnapshotdeliveryprogress** removes all rows in the **MSsnapshotdeliveryprogress** table. This effectively removes all metadata left behind at the subscription database by any previous progress made in the snapshot delivery processes.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_resetsnapshotdeliveryprogress**.  
  
## See Also  
 [Replication Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
