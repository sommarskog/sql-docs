---
title: "Change the account for SSIS Scale Out logging"
description: "Learn how to change the account you use for SQL Server Integration Services (SSIS) Scale Out logging."
author: "haoqian"
ms.author: "haoqian"
ms.reviewer: maghan
ms.date: 06/29/2020
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
ms.custom: performance
---
# Change the account for Scale Out logging

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


When you run SSIS packages in Scale Out, the event messages are logged in the SSISDB database with an auto-created user account named **##MS_SSISLogDBWorkerAgentLogin##**. The login for this user uses SQL Server authentication.

If you want to change the account used for Scale Out logging, do the following things:

> [!NOTE]
> If you use a Windows user account for logging, use the same account as the account that runs the Scale Out Worker service. Otherwise, the login to SQL Server fails.

## 1. Create a user for SSISDB
For instructions about how to create a database user, see [Create a Database User](../../relational-databases/security/authentication-access/create-a-database-user.md).

## 2. Add the user to the database role ssis_cluster_worker

For instructions about how to join a database role, see [Join a Role](../../relational-databases/security/authentication-access/join-a-role.md).

## 3. Update the logging information in SSISDB
Call the stored procedure `[catalog].[update_logdb_info]` with the SQL Server name and connection string as parameters, as shown in the following example:

```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## 4. Restart the Scale Out Worker service
Restart the Scale Out Worker service to make the change effective.

## Next steps
-   [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)
