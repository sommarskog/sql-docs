---
title: "sys.sp_rda_set_rpo_duration (Transact-SQL)"
description: Learn about sys.sp_rda_set_rpo_duration. Use this stored procedure to set the number of hours of migrated data that SQL Server retains in a staging table.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 06/26/2023
ms.service: sql
ms.subservice: stored-procedures
ms.topic: "reference"
f1_keywords:
  - "sys.sp_rda_set_rpo_duration"
  - "sys.sp_rda_set_rpo_duration_TSQL"
helpviewer_keywords:
  - "sys.sp_rda_set_rpo_duration stored procedure"
dev_langs:
  - "TSQL"
---
# sys.sp_rda_set_rpo_duration (Transact-SQL)

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

Sets the number of hours of migrated data that SQL Server retains in a staging table, to help ensure a full restore of the remote Azure database, if a point in time restore is necessary.

For more info, see [Stretch Database reduces the risk of data loss for your Azure data by retaining migrated rows temporarily](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO).

> [!IMPORTANT]  
> Stretch Database is deprecated in [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)]. [!INCLUDE [ssNoteDepFutureAvoid-md](../../includes/ssnotedepfutureavoid-md.md)]

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs
[ ; ]
```

## Arguments

#### [ @duration_hrs = ] *duration_hrs*

The number of hours (a non-null **integer** value) of migrated data that you want SQL Server to retain for the current Stretch-enabled database. The default value, which is also the minimum value, is 8 hours.

> [!NOTE]  
> Higher values require more storage space on SQL Server.

## Permissions

Requires **db_owner** permissions.

## Remarks

Get the current value by running [sys.sp_rda_get_rpo_duration (Transact-SQL)](sys-sp-rda-get-rpo-duration-transact-sql.md).

## See also

- [sys.sp_rda_get_rpo_duration (Transact-SQL)](sys-sp-rda-get-rpo-duration-transact-sql.md)
- [Restore Stretch-enabled databases (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)
- [Stretch Database](../../sql-server/stretch-database/stretch-database.md)
