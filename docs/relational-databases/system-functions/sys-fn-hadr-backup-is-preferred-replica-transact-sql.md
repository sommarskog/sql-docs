---
title: "sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)"
description: "sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/16/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.fn_hadr_backup_is_preferred_replica_TSQL"
  - "sys.fn_hadr_backup_is_preferred_replica"
  - "fn_hadr_backup_is_preferred_replica_TSQL"
  - "fn_hadr_backup_is_preferred_replica"
helpviewer_keywords:
  - "backup on secondary replicas"
  - "active secondary replicas [SQL Server], backup on secondary replicas"
  - "sys.fn_hadr_backup_is_preferred_replica function"
dev_langs:
  - "TSQL"
---
# sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Used to determine if the current replica is the preferred backup replica.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## Arguments  
 '*dbname*'  
 Is the name of the database to be backed up. *dbname* is type sysname.  
  
## Returns  
 Returns data type **bool**: 1 if the database on the current instance is on the preferred replica, otherwise 0.  
  
## Remarks  
 Use this function in a backup script to determine if the current database is on the replica that is preferred for backups. You can run a script on every availability replica. Each of these jobs looks at the same data to determine which job should run, so only one of the scheduled jobs actually proceeds to the backup stage. Sample code could be similar to the following.  
  
```sql  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).
      Select 'This is not the preferred replica, exiting with success';  
END  
-- If this is the preferred replica, continue to do the backup.  
  /* actual backup command goes here */
```  
  
## Examples  
  
### A. Using sys.fn_hadr_backup_is_preferred_replica  
 The following example returns 1 if the current database is the preferred backup replica.  
  
```sql
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> Related Tasks  
  
-   [Configure Backup on Availability Replicas &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## See Also  
 [Always On Availability Groups Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On Availability Groups &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Active Secondaries: Backup on Secondary Replicas &#40;Always On Availability Groups&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)    [Always On Availability Groups Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
