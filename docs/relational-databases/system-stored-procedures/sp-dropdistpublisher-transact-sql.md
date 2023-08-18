---
title: "sp_dropdistpublisher (Transact-SQL)"
description: "sp_dropdistpublisher (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_dropdistpublisher"
  - "sp_dropdistpublisher_TSQL"
helpviewer_keywords:
  - "sp_dropdistpublisher"
dev_langs:
  - "TSQL"
---
# sp_dropdistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Drops a distribution Publisher. This stored procedure is executed at the Distributor on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the Publisher to drop. *publisher* is **sysname**, with no default.  
 
> [!NOTE]
>  Using a custom port for the SQL Server publisher was introduced in SQL Server 2019. If the SQL Server publisher is configured with a custom port, then when dropping such a publisher on the distributor, supply the publisher server name instead of `<Hostname>,<PortNumber>`. 
  
`[ @no_checks = ] no_checks`
 Specifies whether **sp_dropdistpublisher** checks that the Publisher has uninstalled the server as the Distributor. *no_checks* is **bit**, with a default of **0**.  
  
 If **0**, replication verifies that the remote Publisher has uninstalled the local server as the Distributor. If the Publisher is local, replication verifies that there are no publication or distribution objects remaining on the local server.  
  
 If **1**, all the replication objects associated with the distribution Publisher are dropped even if a remote Publisher cannot be reached. After doing this, the remote Publisher must uninstall replication using [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) with **\@ignore_distributor** = **1**.  
  
`[ @ignore_distributor = ] ignore_distributor`
 Specifies whether distribution objects are left at the Distributor when the Publisher is removed. *ignore_distributor* is **bit** and can be one of these values:  
  
 **1** = distribution objects belonging to the *publisher* remain at the Distributor.  
  
 **0** = distribution objects for the *publisher* are cleaned-up at the Distributor.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_dropdistpublisher** is used in all types of replication.  
  
 When dropping an Oracle Publisher, if unable to drop the Publisher **sp_dropdistpublisher** returns an error and the Distributor objects for the Publisher are removed.  
  
## Example  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_dropdistpublisher**.  
  
## See Also  
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Replication Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
