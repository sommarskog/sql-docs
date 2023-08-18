---
title: "sp_getapplock (Transact-SQL)"
description: "sp_getapplock (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_getapplock_TSQL"
  - "sp_getapplock"
helpviewer_keywords:
  - "application locks"
  - "sp_getapplock"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sp_getapplock (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Places a lock on an application resource.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_getapplock [ @Resource = ] 'resource_name' ,  
     [ @LockMode = ] 'lock_mode'   
     [ , [ @LockOwner = ] 'lock_owner' ]   
     [ , [ @LockTimeout = ] 'value' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## Arguments  
 [ @Resource= ] '*resource_name*'  
 Is a string specifying a name that identifies the lock resource. The application must ensure that the resource name is unique. The specified name is hashed internally into a value that can be stored in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lock manager. *resource_name* is **nvarchar(255)** with no default. If a resource string is longer than **nvarchar(255)**, it will be truncated to **nvarchar(255)**.  
  
 *resource_name* is binary compared, and thus is case-sensitive regardless of the collation settings of the current database.  
  
> [!NOTE]  
>  After an application lock has been acquired, only the first 32 characters can be retrieved in plain text; the remainder will be hashed.  
  
 [ @LockMode= ] '*lock_mode*'  
 Is the lock mode to be obtained for a particular resource. *lock_mode* is **varchar(32)** and has no default value. The value can be any of the following: **Shared**, **Update**, **IntentShared**, **IntentExclusive**, or **Exclusive**. For more information, see [lock modes](../sql-server-transaction-locking-and-row-versioning-guide.md#lock_modes).
  
 [ @LockOwner= ] '*lock_owner*'  
 Is the owner of the lock, which is the *lock_owner* value when the lock was requested. *lock_owner* is **varchar(32)**. The value can be **Transaction** (the default) or **Session**. When the *lock_owner* value is **Transaction**, by default or specified explicitly, sp_getapplock must be executed from within a transaction.  
  
 [ @LockTimeout= ] '*value*'  
 Is a lock time-out value in milliseconds. The default value is the same as the value returned by @@LOCK_TIMEOUT. A value of -1 (default) indicates no time-out period (that is, wait forever). To indicate that a lock request should return a Return Code of -1 instead of wait for the lock when the request cannot be granted immediately, specify 0.  
  
 [ @DbPrincipal= ] '*database_principal*'  
 Is the user, role, or application role that has permissions to an object in a database. The caller of the function must be a member of *database_principal*, dbo, or the db_owner fixed database role to call the function successfully. The default is public.  
  
## Return Code Values  
 \>= 0 (success), or < 0 (failure)  
  
|Value|Result|  
|-----------|------------|  
|0|The lock was successfully granted synchronously.|  
|1|The lock was granted successfully after waiting for other incompatible locks to be released.|  
|-1|The lock request timed out.|  
|-2|The lock request was canceled.|  
|-3|The lock request was chosen as a deadlock victim.|  
|-999|Indicates a parameter validation or other call error.|  
  
## Remarks  
 Locks placed on a resource are associated with either the current transaction or the current session. Locks associated with the current transaction are released when the transaction commits or rolls back. Locks associated with the session are released when the session is logged out. When the server shuts down for any reason, all locks are released.  
  
 The lock resource created by sp_getapplock is created in the current database for the session. Each lock resource is identified by the combined values of:  
  
-   The database ID of the database containing the lock resource.  
  
-   The database principal specified in the @DbPrincipal parameter.  
  
-   The lock name specified in the @Resource parameter.  
  
 Only a member of the database principal specified in the @DbPrincipal parameter can acquire application locks that specify that principal. Members of the dbo and db_owner roles are implicitly considered members of all roles.  
  
 Locks can be explicitly released with sp_releaseapplock. When an application calls sp_getapplock multiple times for the same lock resource, sp_releaseapplock must be called the same number of times to release the lock.  When a lock is opened with the `Transaction` lock owner, that lock is released when the transaction is committed or rolled back.
  
 If sp_getapplock is called multiple times for the same lock resource, but the lock mode that is specified in any of the requests is not the same as the existing mode, the effect on the resource is a union of the two lock modes. In most cases, this means the lock mode is promoted to the stronger of the lock modes, the existing mode, or the newly requested mode. This stronger lock mode is held until the lock is ultimately released even if lock release calls have occurred before that time. For example, in the following sequence of calls, the resource is held in `Exclusive` mode instead of in `Shared` mode.  
  
```  
USE AdventureWorks2022;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
EXEC @result = sp_releaseapplock @Resource = 'Form1';  
COMMIT TRANSACTION;  
GO  
```  
  
 A deadlock with an application lock does not roll back the transaction that requested the application lock. Any rollback that might be required as a result of the return value must be done manually. Consequently, we recommend that error checking be included in the code so that if certain values are returned (for example, -3), a ROLLBACK TRANSACTION or alternative action is initiated.  
  
 Here is an example:  
  
```  
USE AdventureWorks2022;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
IF @result = -3  
BEGIN  
    ROLLBACK TRANSACTION;  
END  
ELSE  
BEGIN  
    EXEC @result = sp_releaseapplock @Resource = 'Form1';  
    COMMIT TRANSACTION;  
END;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uses the current database ID to qualify the resource. Therefore, if sp_getapplock is executed, even with identical parameter values on different databases, the result is separate locks on separate resources.  
  
 Use the sys.dm_tran_locks dynamic management view or the sp_lock system stored procedure to examine lock information, or use [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] to monitor locks.  
  
## Permissions  
 Requires membership in the public role.  
  
## Examples  
 The following example places a shared lock, which is associated with the current transaction, on the resource `Form1` in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database.  
  
```  
USE AdventureWorks2022;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
 The following example specifies `dbo` as the database principal.  
  
```  
BEGIN TRAN;  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'AdventureWorks2022',   
     @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
## See Also  
 [APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)  
  
  
