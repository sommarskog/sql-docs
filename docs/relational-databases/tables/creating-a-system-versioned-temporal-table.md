---
title: Create a system-versioned temporal table
description: "Create a system-versioned temporal table. There are three ways to create a system-versioned temporal table."
author: rwestMSFT
ms.author: randolphwest
ms.date: 06/22/2023
ms.service: sql
ms.subservice: table-view-index
ms.topic: conceptual
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Create a system-versioned temporal table

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

There are three ways to create a system-versioned temporal table when considering how the history table is specified:

- Temporal table with an anonymous history table: you specify the schema of the current table and let the system create a corresponding history table with auto-generated name.

- Temporal table with a default history table: you specify the history table schema name and table name and let the system create a history table in that schema.

- Temporal table with a user-defined history table created beforehand: you create a history table that fits best your needs and then reference that table during temporal table creation.

## <a id="#creating-a-temporal-table-with-an-anonymous-history-table"></a> Create a temporal table with an anonymous history table

Creating a temporal table with an "anonymous" history table is a convenient option for quick object creation, especially in prototypes and test environments. It's also the simplest way to create a temporal table since it doesn't require any parameter in `SYSTEM_VERSIONING` clause. In the following example, a new table is created with system-versioning enabled without defining the name of the history table.

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED,
    DeptName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDeptID INT NULL,
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON);
```

### Remarks

- A system-versioned temporal table must have a primary key defined and have exactly one `PERIOD FOR SYSTEM_TIME` defined with two **datetime2** columns, declared as `GENERATED ALWAYS AS ROW START` or `GENERATED ALWAYS AS ROW END`.

- The `PERIOD` columns are always assumed to be non-nullable, even if nullability isn't specified. If the `PERIOD` columns are explicitly defined as nullable, the `CREATE TABLE` statement fails.

- The history table must always be schema-aligned with the current or temporal table, with respect to the number of columns, column names, ordering and data types.

- An anonymous history table is automatically created in the same schema as current or temporal table.

- The anonymous history table name has the following format: *MSSQL_TemporalHistoryFor_<current_temporal_table_object_id>_[suffix]*. Suffix is optional and is added only if the first part of the table name isn't unique.

- The history table is created as a rowstore table. PAGE compression is applied if possible, otherwise the history table is uncompressed. For example, some table configurations, such as SPARSE columns, don't allow compression.

- A default clustered index is created for the history table with an auto-generated name in format *IX_<history_table_name>*. The clustered index contains the `PERIOD` columns (end, start).

- To create the current table as a memory-optimized table, see [System-Versioned Temporal Tables with Memory-Optimized Tables](system-versioned-temporal-tables-with-memory-optimized-tables.md).

## <a id="creating-a-temporal-table-with-a-default-history-table"></a> Create a temporal table with a default history table

Creating a temporal table with a default history table is a convenient option when you want to control naming and still rely on the system to create the history table with the default configuration. In the following example, a new table is created with system-versioning enabled with the name of the history table explicitly defined.

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED,
    DeptName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDeptID INT NULL,
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### Remarks

The history table is created using the same rules as apply to creating an "anonymous" history table, with the following rules that apply specifically to the named history table.

- The schema name is mandatory for the `HISTORY_TABLE` parameter.
- If the specified schema doesn't exist, the `CREATE TABLE` statement fails.
- If the table specified by the `HISTORY_TABLE` parameter already exists, it is validated against the newly created temporal table in terms of [schema consistency and temporal data consistency](./temporal-tables.md). If you specify an invalid history table, the `CREATE TABLE` statement fails.

## <a id="creating-a-temporal-table-with-a-user-defined-history-table"></a> Create a temporal table with a user-defined history table

Creating a temporal table with user-defined history table is a convenient option when the user wants to specify a history table with specific storage options and different indexes tuned to historical queries. In the following example, a user-defined history table is created with a schema that is aligned with the temporal table that is created. To this user-defined history table, a clustered columnstore index and an additional nonclustered rowstore (B+ tree) index is created for point lookups. After this user-defined history table is created, the system-versioned temporal table is created specifying the user-defined history table as the default history table.

```sql
CREATE TABLE DepartmentHistory
(
    DeptID INT NOT NULL,
    DeptName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDeptID INT NULL,
    ValidFrom DATETIME2 NOT NULL,
    ValidTo DATETIME2 NOT NULL
);
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory ON DepartmentHistory;

CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_Period_Columns ON DepartmentHistory (
    ValidTo,
    ValidFrom,
    DeptID
    );
GO

CREATE TABLE Department
(
    DeptID int NOT NULL PRIMARY KEY CLUSTERED,
    DeptName VARCHAR(50) NOT NULL,
    ManagerID INT NULL,
    ParentDeptID INT NULL,
    ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL,
    ValidTo DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL,
    PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### Remarks

- If you plan to run analytic queries on the historical data that employs aggregates or windowing functions, creating a clustered columnstore as a primary index is highly recommended for compression and query performance.
- If the primary use case is for data audit (that is, searching for historical changes for a single row from the current table), then a good choice is to create rowstore history table with a clustered index
- The history table can't have a primary key, foreign keys, unique indexes, table constraints or triggers. It can't be configured for change data capture, change tracking, transactional or merge replication.

## Alter non-temporal table to be a system-versioned temporal table

You can enable system-versioning on an existing non-temporal table, such as when you wish to migrate a custom temporal solution to built-in support.
For example, you may have a set of tables where versioning is implemented with triggers. Using temporal system-versioning is less complex and provides other benefits including:

- Immutable history
- New syntax for time-traveling queries
- Better DML performance
- Minimal maintenance costs

When converting an existing table, consider using the `HIDDEN` clause to hide the new `PERIOD` columns (the **datetime2** columns `ValidFrom` and `ValidTo`) to avoid affecting existing applications that don't explicitly specify column names (for example, `SELECT *` or `INSERT` without column list) aren't designed to handle new columns.

### <a id="adding-versioning-to-non-temporal-tables"></a> Add versioning to non-temporal tables

If you want to start tracking changes for a non-temporal table that contains the data, you need to add the `PERIOD` definition and optionally provide a name for the empty history table that SQL Server creates for you:

```sql
CREATE SCHEMA History;
GO

ALTER TABLE InsurancePolicy
    ADD
        ValidFrom DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN
            CONSTRAINT DF_InsurancePolicy_ValidFrom DEFAULT SYSUTCDATETIME(),
        ValidTo DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN
            CONSTRAINT DF_InsurancePolicy_ValidTo DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.9999999'),
    PERIOD FOR SYSTEM_TIME(ValidFrom, ValidTo);
GO

ALTER TABLE InsurancePolicy
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy));
GO
```

> [!IMPORTANT]  
> The precision for `DATETIME2` must align with the precision for the underlying table. See the following remarks.

#### Remarks

- Adding non-nullable columns with defaults to an existing table with data is a size of data operation on all editions other than SQL Server Enterprise edition (on which it's a metadata operation). With a large existing history table with data on SQL Server Standard edition, adding a non-null column can be an expensive operation.
- Constraints for period start and period end columns must be carefully chosen:
  - Default for start column specifies from which point in time you consider existing rows to be valid. It can't be specified as a datetime point in the future.
  - End time must be specified as the maximum value for a given **datetime2** precision, for example `9999-12-31 23:59:59` or `9999-12-31 23:59:59.9999999`.
- Adding `PERIOD` performs a data consistency check on current table to make sure that the existing values for period columns are valid.
- When an existing history table is specified when enabling `SYSTEM_VERSIONING`, a data consistency check is performed across both the current and the history table. It can be skipped if you specify `DATA_CONSISTENCY_CHECK = OFF` as an additional parameter.

### Migrate existing tables to built-in support

This example shows how to migrate from an existing solution based on triggers to built-in temporal support. For this example, we assume that the current custom solution splits the current and historical data in two separate user tables (`ProjectTaskCurrent` and `ProjectTaskHistory`).

If your existing solution uses single table to store actual and historical rows, then you should split the data into two tables prior to the migration steps shown in following example. First, drop the trigger on the future temporal table. Then, ensure the `PERIOD` columns are non-nullable.

```sql
/* Drop trigger on future temporal table */
DROP TRIGGER ProjectCurrent_OnUpdateDelete;

/* Make sure that future period columns are non-nullable */
ALTER TABLE ProjectTaskCurrent
ALTER COLUMN [ValidFrom] DATETIME2 NOT NULL;

ALTER TABLE ProjectTaskCurrent
ALTER COLUMN [ValidTo] DATETIME2 NOT NULL;

ALTER TABLE ProjectTaskHistory
ALTER COLUMN [ValidFrom] DATETIME2 NOT NULL;

ALTER TABLE ProjectTaskHistory
ALTER COLUMN [ValidTo] DATETIME2 NOT NULL;

ALTER TABLE ProjectTaskCurrent ADD PERIOD
FOR SYSTEM_TIME([ValidFrom], [ValidTo]);

ALTER TABLE ProjectTaskCurrent SET (
    SYSTEM_VERSIONING = ON (
        HISTORY_TABLE = dbo.ProjectTaskHistory,
        DATA_CONSISTENCY_CHECK = ON
    )
);
```

#### Remarks

- Referencing existing columns in `PERIOD` definition implicitly changes `generated_always_type` to `AS_ROW_START` and `AS_ROW_END` for those columns.
- Adding `PERIOD` performs a data consistency check on current table to make sure that the existing values for period columns are valid
- It's highly recommended to set `SYSTEM_VERSIONING` with `DATA_CONSISTENCY_CHECK = ON` to enforce data consistency checks on existing data.
- If hidden columns are preferred, use the command `ALTER TABLE [tableName] ALTER COLUMN [columnName] ADD HIDDEN;`.

## Next steps

- [Temporal tables](temporal-tables.md)
- [Getting Started with system-versioned temporal tables](getting-started-with-system-versioned-temporal-tables.md)
- [Manage retention of historical data in system-versioned temporal tables](manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [System-Versioned Temporal Tables with Memory-Optimized Tables](system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)
- [Modifying data in a system-versioned temporal table](modifying-data-in-a-system-versioned-temporal-table.md)
- [Querying data in a system-versioned temporal table](querying-data-in-a-system-versioned-temporal-table.md)
- [Changing the schema of a system-versioned temporal table](changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Stopping system-versioning on a system-versioned temporal table](stopping-system-versioning-on-a-system-versioned-temporal-table.md)
