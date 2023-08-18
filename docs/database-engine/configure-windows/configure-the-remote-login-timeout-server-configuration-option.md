---
title: "Configure the remote login timeout (server configuration option)"
description: "Learn about the remote login timeout option. See how it limits the number of seconds that SQL Server allots for connecting to a remote server."
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/02/2017"
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "remote login timeout option"
---
# Configure the remote login timeout (server configuration option)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  This topic describes how to configure the **remote login timeout** server configuration option in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)]. The **remote login timeout** option specifies the number of seconds to wait before returning from a failed attempt to log in to a remote server. For example, if you are trying to log in to a remote server and that server is down, **remote login timeout** helps make sure that you do not have to wait indefinitely before your computer stops trying to log in. The default value for this option is 10 seconds. A value of 0 allows for an infinite wait.  
  
> [!NOTE]  
>  The default value for this option is 20 seconds in [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)].  
  
 **In This Topic**  
  
-   **Before you begin:**  
  
     [Limitations and Restrictions](#Restrictions)  
  
     [Security](#Security)  
  
-   **To configure the remote login timeout option, using:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After you configure the remote login timeout option](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
###  <a name="Restrictions"></a> Limitations and Restrictions  
  
-   The **remote login timeout** option affects connections to OLE DB providers made for heterogeneous queries.  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 Execute permissions on **sp_configure** with no parameters or with only the first parameter are granted to all users by default. To execute **sp_configure** with both parameters to change a configuration option or to run the RECONFIGURE statement, a user must be granted the ALTER SETTINGS server-level permission. The ALTER SETTINGS permission is implicitly held by the **sysadmin** and **serveradmin** fixed server roles.  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To configure the remote login timeout option  
  
1.  In Object Explorer, right-click a server and select **Properties**.  
  
2.  Click the **Advanced** node.  
  
3.  Under **Network**, select a value for the **Remote Login Timeout** box.  
  
     Use the **remote login timeout** option to specify the number of seconds to wait before returning from a failed remote login attempt.  
  
##  <a name="TsqlProcedure"></a> Using Transact-SQL  
  
#### To configure the remote login timeout option  
  
1.  Connect to the [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  From the Standard bar, click **New Query**.  
  
3.  Copy and paste the following example into the query window and click **Execute**. This example shows how to use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) to set the value of the `remote login timeout` option to `35` seconds.  
  
```sql  
USE AdventureWorks2022;  
GO  
EXEC sp_configure 'remote login timeout', 35 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 For more information, see [Server Configuration Options &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Follow Up: After you configure the remote login timeout option  
 The setting takes effect immediately without restarting the server.  
  
## See Also  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Server Configuration Options &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
