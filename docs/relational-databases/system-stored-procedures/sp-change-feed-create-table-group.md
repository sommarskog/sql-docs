---
title: "sp_change_feed_create_table_group (Transact-SQL)"
description: "The sp_change_feed_create_table_group system stored procedure enables the creation of new change feed table group within the current database"
author: IdrisMotiwala
ms.author: imotiwala
ms.reviewer: wiassaf, randolphwest
ms.date: 06/13/2023
ms.service: synapse-analytics
ms.topic: "reference"
f1_keywords:
  - "sp_change_feed_create_table_group_TSQL"
  - "sp_change_feed_create_table_group_db"
helpviewer_keywords:
  - "sp_change_feed_create_table_group"
dev_langs:
  - "TSQL"
monikerRange: ">=sql-server-ver16 || =azuresqldb-current"
---
# sp_change_feed_create_table_group (Transact-SQL)

[!INCLUDE [sqlserver2022-asdb](../../includes/applies-to-version/sqlserver2022-asdb.md)]

Creates a source to maintain metadata specific to each table group.

A table group represents the container for all the individual tables that will be replicated to the landing zone for [Azure Synapse Link for SQL](/azure/synapse-analytics/synapse-link/sql-synapse-link-overview). For more information, see [Manage Azure Synapse Link for SQL Server and Azure SQL Database](../../sql-server/synapse-link/synapse-link-sql-server-change-feed-manage.md).

> [!NOTE]  
> This stored procedure is used internally and is not recommended for direct administrative use. Use Synapse Studio instead. Using this procedure will introduce inconsistency with Synapse Workspace configuration.

## Syntax

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

```syntaxsql
EXECUTE sys.sp_change_feed_create_table_group
    @table_group_id
    , @table_group_name
    , @workspace_id
    , @destination_location
    , @destination_credential
[ ; ]
```

## Arguments

#### @table_group_id

The unique identifier of the table group.

#### @table_group_name

The name of the table group.

#### @workspace_id

Azure resourceID for the Synapse Workspace requesting creation of the new table group.

#### @destination_location

URL string of the landing zone folder.

#### @destination_credential

The credential name to access the landing zone.

## Permissions

A user with [CONTROL database permissions](../security/permissions-database-engine.md), **db_owner** database role membership, or **sysadmin** server role membership can execute this procedure.

## See also

- [What is Azure Synapse Link for SQL?](/azure/synapse-analytics/synapse-link/sql-synapse-link-overview)
- [sp_change_feed_enable_db (Transact-SQL)](sp-change-feed-enable-db.md)
- [sp_change_feed_disable_db (Transact-SQL)](sp-change-feed-disable-db.md)
- [sp_change_feed_drop_table_group (Transact-SQL)](sp-change-feed-drop-table-group.md)

## Next steps

- [Manage Azure Synapse Link for SQL Server and Azure SQL Database](../../sql-server/synapse-link/synapse-link-sql-server-change-feed-manage.md)
- [Get started with Azure Synapse Link for SQL Server 2022](/azure/synapse-analytics/synapse-link/connect-synapse-link-sql-server-2022)
