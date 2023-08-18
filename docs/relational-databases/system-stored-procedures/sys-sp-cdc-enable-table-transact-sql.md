---
title: "sys.sp_cdc_enable_table (Transact-SQL)"
description: "Enables change data capture for the specified source table in the current database."
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 06/30/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.sp_cdc_enable_table_TSQL"
  - "sp_cdc_enable_table_TSQL"
  - "sys.sp_cdc_enable_table"
  - "sp_cdc_enable_table"
helpviewer_keywords:
  - "change data capture [SQL Server], enabling tables"
  - "sys.sp_cdc_enable_table"
  - "sp_cdc_enable_table"
dev_langs:
  - "TSQL"
---
# sys.sp_cdc_enable_table (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Enables change data capture for the specified source table in the current database. When a table is enabled for change data capture, a record of each data manipulation language (DML) operation applied to the table is written to the transaction log. The change data capture process retrieves this information from the log and writes it to change tables that are accessed by using a set of functions.

Change data capture isn't available in every edition of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of features that are supported by the editions of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)], see [Editions and supported features of SQL Server 2022](../../sql-server/editions-and-components-of-sql-server-2022.md).

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sys.sp_cdc_enable_table
    [ @source_schema = ] 'source_schema'
      , [ @source_name = ] 'source_name'
    [ , [ @capture_instance = ] 'capture_instance' ]
    [ , [ @supports_net_changes = ] supports_net_changes ]
      , [ @role_name = ] 'role_name'
    [ , [ @index_name = ] 'index_name' ]
    [ , [ @captured_column_list = ] N'captured_column_list' ]
    [ , [ @filegroup_name = ] 'filegroup_name' ]
    [ , [ @allow_partition_switch = ] 'allow_partition_switch' ]
[ ; ]
```

## Arguments

#### [ @source_schema = ] '*source_schema*'

The name of the schema in which the source table belongs. *@source_schema* is **sysname**, with no default, and can't be NULL.

#### [ @source_name = ] '*source_name*'

The name of the source table on which to enable change data capture. *@source_name* is **sysname**, with no default, and can't be NULL.

*source_name* must exist in the current database. Tables in the `cdc` schema can't be enabled for change data capture.

#### [ @role_name = ] '*role_name*'

The name of the database role used to gate access to change data. *@role_name* is **sysname** and must be specified. If explicitly set to NULL, no gating role is used to limit access to the change data.

If the role currently exists, it is used. If the role doesn't exist, an attempt is made to create a database role with the specified name. The role name is trimmed of white space at the right of the string before attempting to create the role. If the caller isn't authorized to create a role within the database, the stored procedure operation fails.

#### [ @capture_instance = ] '*capture_instance*'

The name of the capture instance used to name instance-specific change data capture objects. *@capture_instance* is **sysname** and can't be NULL.

If not specified, the name is derived from the source schema name plus the source table name in the format `<schemaname>_<sourcename>`. *@capture_instance* can't exceed 100 characters and must be unique within the database. Whether specified or derived, *@capture_instance* is trimmed of any white space to the right of the string.

A source table can have a maximum of two capture instances. For more information, see, [sys.sp_cdc_help_change_data_capture (Transact-SQL)](sys-sp-cdc-help-change-data-capture-transact-sql.md).

#### [ @supports_net_changes = ] *supports_net_changes*

Indicates whether support for querying for net changes is to be enabled for this capture instance. *@supports_net_changes* is **bit** with a default of `1` if the table has a primary key or the table has a unique index that has been identified by using the *@index_name* parameter. Otherwise, the parameter defaults to `0`.

- If `0`, only the support functions to query for all changes are generated.
- If `1`, the functions that are needed to query for net changes are also generated.

If *@supports_net_changes* is set to `1`, *@index_name* must be specified, or the source table must have a defined primary key.

When *@supports_net_changes* is set to `1`, an additional nonclustered index is created on the change table, and the net changes query function is created. Because this index needs to be maintained, enabling net changes can have a negative effect on CDC performance.

#### [ @index_name = ] '*index_name*'

The name of a unique index to use to uniquely identify rows in the source table. *@index_name* is **sysname** and can be NULL. If specified, *@index_name* must be a valid unique index on the source table. If *@index_name* is specified, the identified index columns take precedence over any defined primary key columns as the unique row identifier for the table.

#### [ @captured_column_list = ] N'*captured_column_list*'

Identifies the source table columns that are to be included in the change table. *@captured_column_list* is **nvarchar(max)** and can be NULL. If NULL, all columns are included in the change table.

Column names must be valid columns in the source table. Columns defined in a primary key index, or columns defined in an index referenced by *@index_name* must be included.

*@captured_column_list* is a comma-separated list of column names. Individual column names within the list can be optionally quoted by using either double quotation marks (`""`) or square brackets (`[]`). If a column name contains an embedded comma, the column name must be quoted.

*@captured_column_list* can't contain the following reserved column names: `__$start_lsn`, `__$end_lsn`, `__$seqval`, `__$operation`, and `__$update_mask`.

#### [ @filegroup_name = ] '*filegroup_name*'

The filegroup to be used for the change table created for the capture instance. *@filegroup_name* is **sysname** and can be NULL. If specified, *@filegroup_name* must be defined for the current database. If NULL, the default filegroup is used.

We recommend creating a separate filegroup for change data capture change tables.

#### [ @allow_partition_switch = ] '*allow_partition_switch*'

Indicates whether the SWITCH PARTITION command of ALTER TABLE can be executed against a table that is enabled for change data capture. *@allow_partition_switch* is **bit**, with a default of `1`.

For nonpartitioned tables, the switch setting is always 1, and the actual setting is ignored. If the switch is explicitly set to `0` for a nonpartitioned table, warning 22857 is issued to indicate that the switch setting has been ignored. If the switch is explicitly set to `0` for a partitioned table, the warning 22356 is issued to indicate that partition switch operations on the source table are disallowed. Finally, if the switch setting is either set explicitly to `1` or allowed to default to `1` and the enabled table is partitioned, warning 22855 is issued to indicate that partition switches won't be blocked. If any partition switches occur, change data capture doesn't track the changes resulting from the switch. This causes data inconsistencies when the change data is consumed.

SWITCH PARTITION is a metadata operation, but it causes data changes. The data changes that are associated with this operation aren't captured in the change data capture change tables. Consider a table that has three partitions, and changes are made to this table. The capture process tracks user insert, update, and delete operations that are executed against the table. However, if a partition is switched out to another table (for example, to perform a bulk delete), the rows that were moved as part of this operation aren't captured as deleted rows in the change table. Similarly, if a new partition that has prepopulated rows is added to the table, these rows aren't reflected in the change table. This can cause data inconsistency when the changes are consumed by an application and applied to a destination.

If you enable partition switching on [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)], you might also need split and merge operations in near future. Before executing a split or merge operation on a replicated or CDC enabled table, ensure that the partition in question doesn't have any pending replicated commands. You should also ensure that no DML operations are executed on the partition during the split and merge operations. If there are transactions which the log reader or CDC capture job hasn't processed, or if DML operations are performed on a partition of a replicated or CDC enabled table while a split or merge operation is executed (involving the same partition), it could lead to a processing error (error 608 - No catalog entry found for partition ID) with log reader agent or CDC capture job. In order to correct the error, it might require a reinitialization of the subscription or disabling CDC on that table or database.

## Return code values

`0` (success) or `1` (failure).

## Result sets

None.

## Remarks

Before you can enable a table for change data capture, the database must be enabled. To determine whether the database is enabled for change data capture, query the `is_cdc_enabled` column in the [sys.databases](../system-catalog-views/sys-databases-transact-sql.md) catalog view. To enable the database, use the [sys.sp_cdc_enable_db](sys-sp-cdc-enable-db-transact-sql.md) stored procedure.

When change data capture is enabled for a table, a change table and one or two query functions are generated. The change table serves as a repository for the source table changes extracted from the transaction log by the capture process. The query functions are used to extract data from the change table. The names of these functions are derived from the *@capture_instance* parameter in the following ways:

- All changes function: `cdc.fn_cdc_get_all_changes_<capture_instance>`
- Net changes function: `cdc.fn_cdc_get_net_changes_<capture_instance>`

`sys.sp_cdc_enable_table` also creates the capture and cleanup jobs for the database if the source table is the first table in the database to be enabled for change data capture and no transactional publications exist for the database. It sets the `is_tracked_by_cdc` column in the [sys.tables](../system-catalog-views/sys-tables-transact-sql.md) catalog view to `1`.

[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Agent doesn't have to be running when CDC is enabled for a table. However, the capture process doesn't process the transaction log and write entries to the change table unless [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Agent is running.

## Permissions

Requires membership in the **db_owner** fixed database role.

## Examples

### A. Enable change data capture by specifying only required parameters

The following example enables change data capture for the `HumanResources.Employee` table. Only the required parameters are specified.

```sql
USE AdventureWorks2022;
GO

EXECUTE sys.sp_cdc_enable_table
    @source_schema = N'HumanResources',
    @source_name = N'Employee',
    @role_name = N'cdc_Admin';
GO
```

### B. Enable change data capture by specifying additional optional parameters

The following example enables change data capture for the `HumanResources.Department` table. All parameters except *@allow_partition_switch* are specified.

```sql
USE AdventureWorks2022;
GO

EXEC sys.sp_cdc_enable_table
    @source_schema = N'HumanResources',
    @source_name = N'Department',
    @role_name = N'cdc_admin',
    @capture_instance = N'HR_Department',
    @supports_net_changes = 1,
    @index_name = N'AK_Department_Name',
    @captured_column_list = N'DepartmentID, Name, GroupName',
    @filegroup_name = N'PRIMARY';
GO
```

## See also

- [sys.sp_cdc_disable_table (Transact-SQL)](sys-sp-cdc-disable-table-transact-sql.md)
- [sys.sp_cdc_help_change_data_capture (Transact-SQL)](sys-sp-cdc-help-change-data-capture-transact-sql.md)
- [cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (Transact-SQL)](../system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)
- [cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact-SQL)](../system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)
- [sys.sp_cdc_help_jobs (Transact-SQL)](sys-sp-cdc-help-jobs-transact-sql.md)
