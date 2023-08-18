---
title: "sp_syscollector_set_cache_window (Transact-SQL)"
description: Sets the number of times to attempt a data upload if a failure occurs.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 07/04/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_syscollector_set_cache_window"
  - "sp_syscollector_set_cache_window_TSQL"
helpviewer_keywords:
  - "sp_syscollector_set_cache_window stored procedure"
  - "data collector [SQL Server], stored procedures"
dev_langs:
  - "TSQL"
---
# sp_syscollector_set_cache_window (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Sets the number of times to attempt a data upload if a failure occurs. Retrying an upload in the event of a failure mitigates the risk of losing collected data.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_syscollector_set_cache_window [ [ @cache_window = ] cache_window ]
[ ; ]
```

## Arguments

#### [ @cache_window = ] *cache_window*

The number of times a failed data upload to the management data warehouse is retried without losing data. *@cache_window* is **int**, with a default of `1`. *@cache_window* can have one of the following values:

| Value | Description |
| --- | --- |
| -1 | Cache all the upload data from the previous upload failures. |
| 0 | Don't cache any data from an upload failure. |
| *n* | Cache data from n previous upload failures, where *n* >= 1. |

## Return code values

`0` (success) or `1` (failure).

## Remarks

You must disable the data collector before changing the cache window configuration. This stored procedure fails if the data collector is enabled. For more information, see [Enable or Disable Data Collection](../data-collection/enable-or-disable-data-collection.md), and [Manage Data Collection](../data-collection/manage-data-collection.md).

## Permissions

Requires membership in the **dc_admin** (with EXECUTE permission) fixed database role to execute this procedure.

## Examples

The following example disables the data collector, configures the cache window to retain data for up to three failed uploads, and then enables to data collector.

```sql
USE msdb;
GO
EXECUTE dbo.sp_syscollector_disable_collector;
GO
EXECUTE dbo.sp_syscollector_set_cache_window 3;
GO
EXECUTE dbo.sp_syscollector_enable_collector;
```

## See also

- [System stored procedures (Transact-SQL)](system-stored-procedures-transact-sql.md)
- [sp_syscollector_set_cache_directory (Transact-SQL)](sp-syscollector-set-cache-directory-transact-sql.md)
