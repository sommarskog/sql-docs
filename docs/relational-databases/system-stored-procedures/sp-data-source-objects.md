---
title: "sp_data_source_objects"
description: "sp_data_source_objects returns list of table objects that are available to be virtualized."
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: wiassaf
ms.date: 06/13/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: conceptual
f1_keywords:
  - "sp_data_source_objects_TSQL"
  - "sys.sp_data_source_objects_TSQL"
  - "sp_data_source_objects"
  - "sys.sp_data_source_objects"
helpviewer_keywords:
  - "PolyBase"
dev_langs:
  - "TSQL"
---
# sp_data_source_objects (Transact-SQL)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

Returns list of table objects that are available to be virtualized.

## Syntax

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

```syntaxsql
sp_data_source_objects
        [ @data_source = ] 'data_source'
    [ , [ @object_root_name = ] 'object_root_name' ]
    [ , [ @max_search_depth = ] max_search_depth ]
    [ , [ @search_options = ] 'search_options' ]
[ ; ]
```

## Arguments

#### [ @data_source = ] '*data_source*'

The name of the external data source to get the metadata from. *@data_source* is `sysname`.

#### [ @object_root_name = ] '*object_root_name*'

This parameter is the root of the name of the object(s) to search for. *@object_root_name* is `nvarchar(max)`, with a default of `NULL`.

This call only returns external objects that begin with the value set for *@object_root_name*.

If an ODBC data source connects to a relational database management system (RDBMS) that uses three-part names, *@object_root_name* can't contain a partial database name. In these cases, the parameter *@object_root_name* should contain all three parts, with the third part being the object name to search.

> [!CAUTION]  
> Due to differences between external data platforms, some platforms do not return any results if the default value of `NULL` is provided. Some treat `NULL` as the lack of a filter. For example, Oracle RDMBS will not return results if `NULL` is provided for *@object_root_name*.

#### [ @max_search_depth = ] *max_search_depth*

This value specifies the maximum depth (in parts) past the *@object_root_name* that we wish to search. *@max_search_depth* is an **int** with a default of `1`.

For example, a *@max_search_depth* of 1, with an *@object_root_name* that is the name of a SQL Server database, would return schemata contained inside the database.

A *@max_search_depth* of `NULL` returns information about *@object_root_name* if it exists and is non-empty, in the case of catalog or schema.

#### [ @search_options = ] '*search_options*'

The `search_options` parameter is nvarchar(max) with a default of `NULL`.

This parameter isn't used but may be implemented in the future.

## Result sets

| Column name | Data type | Description |
| --- | --- | --- |
| `OBJECT_TYPE` | **nvarchar(200)** | The type of the object (Example: TABLE or DATABASE). |
| `OBJECT_NAME` | **nvarchar(max)** | The fully qualified name of the object. Escaped using backend-specific quote character. |
| `OBJECT_LEAF_NAME` | **nvarchar(max)** | The unqualified object name. |
| `TABLE_LOCATION` | **nvarchar(max)** | A valid table location string that could be used for the CREATE EXTERNAL TABLE statement. Is `NULL` if it isn't applicable. |

## Permissions

Requires ALTER ANY EXTERNAL DATA SOURCE permission.

## Remarks

The SQL Server instance must have the [PolyBase](../polybase/polybase-guide.md) feature installed. This procedure was first introduced in SQL Server 2019 CU5.

This stored procedure supports connectors for:

- SQL Server
- Oracle
- Teradata
- MongoDB
- Azure Cosmos DB

The stored procedure doesn't support generic ODBC data source or Hadoop connectors.

The notion of empty vs. non-empty relates to the behavior of the ODBC driver and the [`SQLTables` function](../native-client-odbc-api/sqltables.md). Non-empty indicates an object contains tables, not rows. For example, an empty schema contains no tables in SQL Server. An empty database contains with no tables inside Teradata.

Object types are determined by the external data source's ODBC driver. Each external data source determines what qualifies as a table. This can include database objects like functions in Teradata, or synonyms in Oracle. PolyBase can't connect to some ODBC objects as external tables and will therefore not have a value in the `TABLE_LOCATION` column. Despite the absence of values in `TABLE_LOCATION`, the presence of one of these ODBC objects may make a database or schema non-empty.

Use `sp_data_source_objects` and [sp_data_source_table_columns](sp-data-source-table-columns.md) to discover external objects. These system stored procedures return the schema of tables that are available to be virtualized. Azure Data Studio uses these two stored procedures to support [data virtualization](../../azure-data-studio/extensions/data-virtualization-extension.md). Use [sp_data_source_table_columns](sp-data-source-table-columns.md) to discover external table schemas represented in SQL Server data types.

### External tables to MongoDB collections that contain arrays

To create external tables to MongoDB collections that contain arrays, you should use the [Data Virtualization extension for Azure Data Studio](../../azure-data-studio/extensions/data-virtualization-extension.md) to produce a CREATE EXTERNAL TABLE statement, based on the schema detected by the PolyBase ODBC Driver for MongoDB. The flattening actions are automatically performed by the driver. Alternatively, you can use [sp_data_source_objects (Transact-SQL)](sp-data-source-objects.md) to detect the collection schema (columns) and manually create the external table. The `sp_data_source_table_columns` stored procedure also automatically performs the flattening via the PolyBase ODBC Driver for MongoDB driver. The Data Virtualization extension for Azure Data Studio and `sp_data_source_table_columns` use the same internal stored procedures to query the external schema.

### Data source type specific remarks

- **Teradata**

  Teradata system views don't use row-level security (RLS), and so users can see the existence of tables that they can't query.

- **MongoDB**

  Some earlier versions of MongoDB restrict the ability to list all databases to admin-like users. Users without this permission may get auth errors trying to execute this procedure with a null *@object_root_name*.

- **Oracle**

  Oracle synonyms aren't supported for usage with PolyBase.

## Examples

### SQL Server

The following example returns all databases, schemata, and tables/views

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 3;

EXEC sp_data_source_objects @data_source,
    @object_root_name,
    @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `DATABASE` | `"database"` | `database` | `NULL` |
| `SCHEMA` | `"database"."dbo"` | `dbo` | `NULL` |
| `TABLE` | `"database"."dbo"."customer"` | `customer` | `[database].[dbo].[customer]` |
| `TABLE` | `"database"."dbo"."item"` | `item` | `[database].[dbo].[item]` |
| `TABLE` | `"database"."dbo"."nation"` | `nation` | `[database].[dbo].[nation]` |

The following example returns all databases

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;

EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `DATABASE` | `UserDatabase` | `UserDatabase` | `NULL` |
| `DATABASE` | `master` | `master` | `NULL` |
| `DATABASE` | `msdb` | `msdb` | `NULL` |
| `DATABASE` | `tempdb` | `tempdb` | `NULL` |
| `DATABASE` | `database` | `database` | `NULL` |

The following example returns all schemata in a database

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = N'[database]';

EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `SCHEMA` | `"database"."dbo"` | `dbo` | `NULL` |
| `SCHEMA` | `"database"."INFORMATION_SCHEMA"` | `INFORMATION_SCHEMA` | `NULL` |
| `SCHEMA` | `"database"."sys"` | `sys` | `NULL` |

The following example returns all tables in schema

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = N'[database].[dbo]';

EXEC sp_data_source_objects @data_source, @object_root_name;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `TABLE` | `"database"."dbo"."customer"` | `customer` | `[database].[dbo].[customer]` |
| `TABLE` | `"database"."dbo"."item"` | `item` | `[database].[dbo].[item]` |
| `TABLE` | `"database"."dbo"."nation"` | `nation` | `[database].[dbo].[nation]` |
| `TABLE` | `"database"."dbo"."orders"` | `orders` | `[database].[dbo].[orders]` |
| `TABLE` | `"database"."dbo"."part"` | `part` | `[database].[dbo].[part]` |

### Oracle

The following example returns the complete schemata and tables, functions, views, and etc.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = N'[OracleObjectRoot]';
DECLARE @max_search_depth INT = 2;

EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `VIEW` | `"SYS"."ALL_SQLSET_STATEMENTS"` | `ALL_SQLSET_STATEMENTS` | `[ORACLEOBJECTROOT].[SYS].[ALL_SQLSET_STATEMENTS]` |
| `SYSTEM TABLE` | `"SYS"."BOOTSTRAP$"` | `BOOTSTRAP$` | `[ORACLEOBJECTROOT].[SYS].[BOOTSTRAP$]` |
| `SYNONYM` | `"PUBLIC"."ALL_ALL_TABLES"` | `ALL_ALL_TABLES` | `NULL` |
| `SCHEMA` | `"database"` | `database` | `NULL` |
| `TABLE` | `"database"."customer"` | `customer` | `[ORACLEOBJECTROOT].[database].[customer]` |

### Teradata

The following example returns all databases and tables, functions, views, and etc.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;

EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `FUNCTION` | `"SYSLIB"."ExtractRoles"` | `ExtractRoles` | `NULL` |
| `SYSTEM TABLE` | `"DBC"."UDTCast"` | `UDTCast` | `[DBC].[UDTCast]` |
| `TYPE` | `"SYSUDTLIB"."XML"` | `XML` | `NULL` |
| `DATABASE` | `"database"` | `database` | `NULL` |
| `TABLE` | `"database"."customer"` | `customer` | `[database].[customer]` |

### Mongo DB

The following example returns all databases and tables.

```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @object_root_name NVARCHAR(MAX) = NULL;
DECLARE @max_search_depth INT = 2;

EXEC sp_data_source_objects @data_source, @object_root_name, @max_search_depth;
```

| OBJECT_TYPE | OBJECT_NAME | OBJECT_LEAF_NAME | TABLE_LOCATION |
| --- | --- | --- | --- |
| `DATABASE` | `"database"` | `database` | `NULL` |
| `TABLE` | `"database"."customer"` | `customer` | `[database].[customer]` |
| `TABLE` | `"database"."item"` | `item` | `[database].[item]` |
| `TABLE` | `"database"."nation"` | `nation` | `[database].[nation]` |
| `TABLE` | `"database"."orders"` | `orders` | `[database].[orders]` |

## See also

- [sp_data_source_columns](./sp-data-source-table-columns.md)
- [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)
- [Data Virtualization extension for Azure Data Studio](../../azure-data-studio/extensions/data-virtualization-extension.md)
- [Get started with PolyBase](../polybase/polybase-guide.md)
- [System stored procedures (Transact-SQL)](system-stored-procedures-transact-sql.md)
