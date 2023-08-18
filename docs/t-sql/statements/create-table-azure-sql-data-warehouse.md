---
title: CREATE TABLE
description: "CREATE TABLE creates a new table in Azure Synapse Analytics, Analytics Platform System (PDW), and Microsoft Fabric."
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: vanto, xiaoyul, mariyaali, maghan, kecona
ms.date: 07/16/2023
ms.service: sql
ms.topic: reference
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest||=fabric"
---

# CREATE TABLE

::: moniker range=">=aps-pdw-2016||=azure-sqldw-latest"

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 Creates a new table in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  

 To understand tables and how to use them, see [Tables in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)]](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-overview).

 Discussions about [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] in this article apply to both [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] unless otherwise noted.

> [!NOTE]
> For SQL Server and Azure SQL platforms, visit [CREATE TABLE](create-table-transact-sql.md?view=azuresqldb-current&preserve-view=true) and select your desired product version.
> For reference to [!INCLUDE[fabric-data-warehouse](../../includes/fabric-dw.md)] in [!INCLUDE[microsoft-fabric](../../includes/fabric.md)], visit [CREATE TABLE (Fabric)](create-table-azure-sql-data-warehouse.md?view=fabric&preserve-view=true).

[!INCLUDE[synapse-analytics-od-supported-tables](../../includes/synapse-analytics-od-supported-tables.md)]

 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## Syntax
  
```syntaxsql
-- Create a new table.
CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]
    )  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[;]  

<column_options> ::=
    [ COLLATE Windows_collation_name ]
    [ NULL | NOT NULL ] -- default is NULL
    [ IDENTITY [ ( seed, increment ) ]
    [ <column_constraint> ]

<column_constraint>::=
    {
        DEFAULT constant_expression
        | PRIMARY KEY NONCLUSTERED NOT ENFORCED -- Applies to Azure Synapse Analytics only
        | UNIQUE NOT ENFORCED -- Applies to Azure Synapse Analytics only
    }

<table_option> ::=
    {
       CLUSTERED COLUMNSTORE INDEX -- default for Azure Synapse Analytics 
      | CLUSTERED COLUMNSTORE INDEX ORDER (column [,...n])  
      | HEAP --default for Parallel Data Warehouse
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC
    }  
    {
        DISTRIBUTION = HASH ( distribution_column_name )
      | DISTRIBUTION = HASH ( [distribution_column_name [, ...n]] ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for Azure Synapse Analytics
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )

<data type> ::=
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to Azure Synapse Analytics 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to Azure Synapse Analytics  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to Azure Synapse Analytics  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

## Arguments

#### *database_name*  
 The name of the database that will contain the new table. The default is the current database.  
  
#### *schema_name*  
 The schema for the table. Specifying *schema* is optional. If blank, the default schema is used.  
  
#### *table_name*  
 The name of the new table. To create a local temporary table, precede the table name with `#`.  For explanations and guidance on temporary tables, see [Temporary tables in dedicated SQL pool in Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-temporary). 

#### *column_name*  
 The name of a table column.

### <a id="ColumnOptions"></a> Column options

 `COLLATE` *Windows_collation_name*  
 Specifies the collation for the expression. The collation must be one of the Windows collations supported by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of Windows collations supported by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see [Windows Collation Name (Transact-SQL)](windows-collation-name-transact-sql.md)/).  
  
 `NULL` | `NOT NULL`  
 Specifies whether `NULL` values are allowed in the column. The default is `NULL`.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 Specifies the default column value.  
  
 | Argument | Explanation |
 | -------- | ----------- |
 | *constraint_name* | The optional name for the constraint. The constraint name is unique within the database. The name can be reused in other databases. |
 | *constant_expression* | The default value for the column. The expression must be a literal value or a constant. For example, these constant expressions are allowed: `'CA'`, `4`. These constant expressions aren't allowed: `2+3`, `CURRENT_TIMESTAMP`. |
  
### <a id="TableOptions"></a> Table structure options

For guidance on choosing the type of table, see [Indexing tables in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)]](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-index).
  
 `CLUSTERED COLUMNSTORE INDEX` 
 
Stores the table as a clustered columnstore index. The clustered columnstore index applies to all of the table data. This behavior is the default for [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].
 
 `HEAP`
  Stores the table as a heap. This behavior is the default for [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 `CLUSTERED INDEX` ( *index_column_name* [ ,...*n* ] )  
 Stores the table as a clustered index with one or more key columns. This behavior stores the data by row. Use *index_column_name* to specify the name of one or more key columns in the index.  For more information, see Rowstore Tables in the General Remarks.
 
 `LOCATION = USER_DB`
 This option is deprecated. It's syntactically accepted, but no longer required and no longer affects behavior.   
  
### <a id="TableDistributionOptions"></a> Table distribution options

To understand how to choose the best distribution method and use distributed tables, see [designing distributed tables using dedicated SQL pool in Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-distribute).

For recommendations on the best distribution strategy to use based on your workloads, see the [Synapse SQL Distribution Advisor (Preview)](/azure/synapse-analytics/sql/distribution-advisor).

`DISTRIBUTION = HASH` ( *distribution_column_name* )
Assigns each row to one distribution by hashing the value stored in *distribution_column_name*. The algorithm is deterministic, which means it always hashes the same value to the same distribution.  The distribution column should be defined as NOT NULL because all rows that have NULL are assigned to the same distribution.

`DISTRIBUTION = HASH ( [distribution_column_name [, ...n]] )` 
Distributes the rows based on the hash values of up to eight columns, allowing for more even distribution of the base table data, reducing the data skew over time and improving query performance.

> [!NOTE]
> - To enable the multi-column distribution (MCD) feature, change the database's compatibility level to 50 with this command. For more information on setting the database compatibility level, see [ALTER DATABASE SCOPED CONFIGURATION](./alter-database-scoped-configuration-transact-sql.md). For example: `ALTER DATABASE SCOPED CONFIGURATION SET DW_COMPATIBILITY_LEVEL = 50;`
> - To disable the Multi-Column distribution (MCD) feature, run this command to change the database's compatibility level to AUTO. For example: `ALTER DATABASE SCOPED CONFIGURATION SET DW_COMPATIBILITY_LEVEL = AUTO;` Existing MCD tables will stay but become unreadable. Queries over MCD tables will return this error: `Related table/view is not readable because it distributes data on multiple columns and multi-column distribution is not supported by this product version or this feature is disabled.`
>   - To regain access to MCD tables, enable the feature again.
>   - To load data into a MCD table, use CTAS statement and the data source needs be Synapse SQL tables.  
> - [Generating a script](../../ssms/scripting/generate-scripts-sql-server-management-studio.md) to create MCD tables is currently supported SSMS version 19 and later versions.

`DISTRIBUTION = ROUND_ROBIN`
Distributes the rows evenly across all the distributions in a round-robin fashion. This behavior is the default for [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].

`DISTRIBUTION = REPLICATE`
Stores one copy of the table on each Compute node. For [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], the table is stored on a distribution database on each Compute node. For [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], the table is stored in a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] filegroup that spans the Compute node. This behavior is the default for [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
### <a id="TablePartitionOptions"></a> Table partition options
For guidance on using table partitions, see [Partitioning tables in dedicated SQL pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition).

`PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
Creates one or more table partitions. These partitions are horizontal table slices that allow you to apply operations to subsets of rows regardless of whether the table is stored as a heap, clustered index, or clustered columnstore index. Unlike the distribution column, table partitions don't determine the distribution where each row is stored. Instead, table partitions determine how the rows are grouped and stored within each distribution.  

| Argument | Explanation |
| -------- | ----------- |
|*partition_column_name*| Specifies the column that [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] will use to partition the rows. This column can be any data type. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] sorts the partition column values in ascending order. The low-to-high ordering goes from `LEFT` to `RIGHT` in the `RANGE` specification. |  
| `RANGE LEFT` | Specifies the boundary value belongs to the partition on the left (lower values). The default is LEFT. |
| `RANGE RIGHT` | Specifies the boundary value belongs to the partition on the right (higher values). | 
| `FOR VALUES` ( *boundary_value* [,...*n*] ) | Specifies the boundary values for the partition. *boundary_value* is a constant expression. It can't be NULL. It must either match or be implicitly convertible to the data type of *partition_column_name*. It can't be truncated during implicit conversion so that the size and scale of the value don't match the data type of *partition_column_name*<br></br><br></br>If you specify the `PARTITION` clause, but don't specify a boundary value, [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] creates a partitioned table with one partition. If applicable, you can split the table into two partitions at a later time.<br></br><br></br>If you specify one boundary value, the resulting table has two partitions; one for the values lower than the boundary value and one for the values higher than the boundary value. If you move a partition into a non-partitioned table, the non-partitioned table receives the data, but won't have the partition boundaries in its metadata.| 

 See [Create a partitioned table](#PartitionedTable) in the Examples section.

### Ordered Clustered columnstore index option

Clustered columnstore index (CCI) is the default for creating tables in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].  Data in a CCI is not sorted before being compressed into columnstore segments.  When creating a CCI with ORDER, data is sorted before being added to index segments and query performance can be improved. See [Performance Tuning with Ordered Clustered Columnstore Index](/azure/sql-data-warehouse/performance-tuning-ordered-cci?view=azure-sqldw-latest&preserve-view=true) for details.  

An ordered CCI can be created on columns of any data types supported in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] except for string columns.  

Users can query **column_store_order_ordinal** column in **sys.index_columns** for the column(s) a table is ordered on and the sequence in the ordering.  

Check [Performance tuning with ordered clustered columnstore index](/azure/sql-data-warehouse/performance-tuning-ordered-cci) for details.   

### <a id="DataTypes"></a> Data type

[!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] supports the most commonly used data types. To better understand data types and how to use them, see [Data types for tables in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)]](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-data-types).

>[!NOTE]
>Similar to SQL Server, there is an 8060 byte per row limit. This may become a blocking issue for tables that have many columns, or columns with large data types, such as `nvarchar(max)` or `varbinary(max)`. Inserts or updates that violate the 8060 byte limit will result in error codes 511 or 611. For more information, see [Pages and Extents Architecture Guide](../../relational-databases/pages-and-extents-architecture-guide.md?view=azure-sqldw-latest&preserve-view=true#row-overflow-considerations).

For a table of data type conversions, see the Implicit Conversions section of [CAST and CONVERT (Transact-SQL)](../functions/cast-and-convert-transact-sql.md). For more information, see [Date and Time Data Types and Functions (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md).

The following list of supported data types includes their details and storage bytes:

`datetimeoffset` [ ( *n* ) ]  
 The default value for *n* is 7.  
  
 `datetime2` [ ( *n* ) ]  
Same as `datetime`, except that you can specify the number of fractional seconds. The default value for *n* is `7`.  
  
|*n* value|Precision|Scale|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 Stores date and time of day with 19 to 23 characters according to the Gregorian calendar. The date can contain year, month, and day. The time contains hour, minutes, seconds. As an option, you can display three digits for fractional seconds. The storage size is 8 bytes.  
  
 `smalldatetime`  
 Stores a date and a time. Storage size is 4 bytes.  
  
 `date`  
 Stores a date using a maximum of 10 characters for year, month, and day according to the Gregorian calendar. The storage size is 3 bytes. Date is stored as an integer.  
  
 `time` [ ( *n* ) ]  
 The default value for *n* is `7`.  
  
 `float` [ ( *n* ) ]  
 Approximate number data type for use with floating point numeric data. Floating point data is approximate, which means that not all values in the data type range can be represented exactly. *n* specifies the number of bits used to store the mantissa of the `float` in scientific notation. *n* dictates the precision and storage size. If *n* is specified, it must be a value between `1` and `53`. The default value of *n* is `53`.  
  
| *n* value | Precision | Storage size |  
| --------: | --------: | -----------: |  
| 1-24   | 7 digits  | 4 bytes      |  
| 25-53  | 15 digits | 8 bytes      |  
  
 [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] treats *n* as one of two possible values. If `1`<= *n* <= `24`, *n* is treated as `24`. If `25` <= *n* <= `53`, *n* is treated as `53`.  
  
 The [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] `float` data type complies with the ISO standard for all values of *n* from `1` through `53`. The synonym for double precision is `float(53)`.  
  
 `real` [ ( *n* ) ]  
 The definition of real is the same as float. The ISO synonym for `real` is `float(24)`.  
  
 `decimal` [ ( *precision* [ *, scale* ] ) ] | `numeric` [ ( *precision* [ *, scale* ] ) ]  
 Stores fixed precision and scale numbers.  
  
 *precision*  
 The maximum total number of decimal digits that can be stored, both to the left and to the right of the decimal point. The precision must be a value from `1` through the maximum precision of `38`. The default precision is `18`.  
  
 *scale*  
 The maximum number of decimal digits that can be stored to the right of the decimal point. *Scale* must be a value from `0` through *precision*. You can only specify *scale* if *precision* is specified. The default scale is `0` and so `0` <= *scale* <= *precision*. Maximum storage sizes vary, based on the precision.  
  
| Precision | Storage bytes  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 Data types that represent currency values.  
  
| Data Type | Storage bytes |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` \| `int` \| `smallint` \| `tinyint`  
 Exact-number data types that use integer data. The storage is shown in the following table.  
  
| Data Type | Storage bytes |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 An integer data type that can take the value of `1`, `0`, or `NULL. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] optimizes storage of bit columns. If there are 8 or fewer bit columns in a table, the columns are stored as 1 byte. If there are from 9-16 bit columns, the columns are stored as 2 bytes, and so on.  
  
 `nvarchar` [ ( *n* | `max` ) ]  -- `max` applies only to [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].  
 Variable-length Unicode character data. *n* can be a value from 1 through 4000. `max` indicates that the maximum storage size is 2^31-1 bytes (2 GB). Storage size in bytes is two times the number of characters entered + 2 bytes. The data entered can be zero characters in length.  
  
 `nchar` [ ( *n* ) ]  
 Fixed-length Unicode character data with a length of *n* characters. *n* must be a value from `1` through `4000`. The storage size is two times *n* bytes.  
  
 `varchar` [ ( *n*  | `max` ) ]  -- `max` applies only to [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].   
 Variable-length, non-Unicode character data with a length of *n* bytes. *n* must be a value from `1` to `8000`. `max` indicates that the maximum storage size is 2^31-1 bytes (2 GB). The storage size is the actual length of data entered + 2 bytes.  
  
 `char` [ ( *n* ) ]  
 Fixed-length, non-Unicode character data with a length of *n* bytes. *n* must be a value from `1` to `8000`. The storage size is *n* bytes. The default for *n* is `1`.  
  
 `varbinary` [ ( *n*  | `max` ) ]  -- `max` applies only to [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].  
 Variable-length binary data. *n* can be a value from `1` to `8000`. `max` indicates that the maximum storage size is 2^31-1 bytes (2 GB). The storage size is the actual length of data entered + 2 bytes. The default value for *n* is 7.  
  
 `binary` [ ( *n* ) ]  
 Fixed-length binary data with a length of *n* bytes. *n* can be a value from `1` to `8000`. The storage size is *n* bytes. The default value for *n* is `7`.  
  
 `uniqueidentifier`  
 Is a 16-byte GUID.  

## Permissions

 Creating a table requires permission in the `db_ddladmin` fixed database role, or:
 
 - `CREATE TABLE` permission on the database
 - `ALTER SCHEMA` permission on the schema that will contain the table

Creating a partitioned table requires permission in the `db_ddladmin` fixed database role, or

- `ALTER ANY DATASPACE` permission
  
 The login that creates a local temporary table receives `CONTROL`, `INSERT`, `SELECT`, and `UPDATE` permissions on the table.  
 
## <a id="GeneralRemarks"></a> Remarks
 
For minimum and maximum limits, see [[!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] capacity limits](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-service-capacity-limits). 
 
### Determine the number of table partitions

Each user-defined table is divided into multiple smaller tables that are stored in separate locations called distributions. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] uses 60 distributions. In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], the number of distributions depends on the number of Compute nodes.
 
Each distribution contains all table partitions. For example, if there are 60 distributions and four table partitions plus one empty partition, there will be 300 partitions (5 x 60= 300). If the table is a clustered columnstore index, there will be one columnstore index per partition, which means you will have 300 columnstore indexes.

We recommend using fewer table partitions to ensure each columnstore index has enough rows to take advantage of the benefits of columnstore indexes. For more information, see [Partitioning tables in dedicated SQL pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition) and [Indexes on dedicated SQL pool tables in Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-index).

### Rowstore table (heap or clustered index)

A rowstore table is a table stored in row-by-row order. It's a heap or clustered index. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] creates all rowstore tables with page compression; this behavior isn't user-configurable.

### Columnstore table (columnstore index)

A columnstore table is a table stored in column-by-column order. The columnstore index is the technology that manages data stored in a columnstore table.  The clustered columnstore index doesn't affect how data is distributed. Rather, it affects how the data is stored within each distribution.

To change a rowstore table to a columnstore table, drop all existing indexes on the table and create a clustered columnstore index. For an example, see [CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md).

For more information, see these articles:
- [Columnstore indexes versioned feature summary](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)
- [Indexing tables in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)]](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-index)
- [Columnstore Indexes Guide](../../relational-databases/indexes/columnstore-indexes-overview.md) 

## <a id="LimitationsRestrictions"></a> Limitations and Restrictions

- You can't define a DEFAULT constraint on a distribution column.  
- Table Name cannot be greater than 128 characters.
- Column Name cannot be greater than 128 characters.
  
### Partitions

The partition column can't have a Unicode-only collation. For example, the following statement fails:
  
```sql
CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))
```  

 If *boundary_value* is a literal value that must be implicitly converted to the data type in *partition_column_name*, a discrepancy occurs. The literal value is displayed through the [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] system views, but the converted value is used for [!INCLUDE[tsql](../../includes/tsql-md.md)] operations. 

### Temporary tables

 Global temporary tables that begin with `##` aren't supported.  
  
 Local temporary tables have the following limitations and restrictions:  
  
-   They're visible only to the current session. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] drops them automatically at the end of the session. To drop them explicitly, use the DROP TABLE statement.   
-   They can't be renamed. 
-   They can't have partitions or views.  
-   Their permissions can't be changed. `GRANT`, `DENY`, and `REVOKE` statements can't be used with local temporary tables.   
-   Database console commands are blocked for temporary tables.   
-   If more than one local temporary table is used within a batch, each must have a unique name. If multiple sessions are running the same batch and creating the same local temporary table, [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] internally appends a numeric suffix to the local temporary table name to maintain a unique name for each local temporary table.  

## <a id="LockingBehavior"></a> Locking behavior
 Takes an exclusive lock on the table. Takes a shared lock on the DATABASE, SCHEMA, and SCHEMARESOLUTION objects.  

## <a id="ExamplesColumn"></a> Examples for columns

### <a id="ColumnCollation"></a> A. Specify a column collation
 In the following example, the table `MyTable` is created with two different column collations. By default, the column, `mycolumn1`, has the default collation Latin1_General_100_CI_AS_KS_WS. The column, `mycolumn2` has the collation Frisian_100_CS_AS.  
  
```sql
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  
  
### <a id="DefaultConstraint"></a> B. Specify a DEFAULT constraint for a column

 The following example shows the syntax to specify a default value for a column. The colA column has a default constraint named constraint_colA  and a default value of 0.  
  
```sql
CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```

## <a id="ExamplesTemporaryTables"></a> Examples for temporary tables

### <a id="TemporaryTable"></a> C. Create a local temporary table
 The following example creates a local temporary table named #myTable. The table is specified with a three-part name, which starts with a #.
  
```sql
CREATE TABLE AdventureWorks.dbo.#myTable
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```

## <a id="ExTableStructure"></a> Examples for table structure

### <a name="ClusteredColumnstoreIndex"></a> D. Create a table with a clustered columnstore index  
 The following example creates a distributed table with a clustered columnstore index. Each distribution is stored as a columnstore.  
  
 The clustered columnstore index doesn't affect how the data is distributed; data is always distributed by row. The clustered columnstore index affects how the data is stored within each distribution.  
  
```sql
  CREATE TABLE MyTable
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX
  )  
;  
```  

### <a id="OrderedClusteredColumnstoreIndex"></a> E. Create an ordered clustered columnstore index

The following example shows how to create an ordered clustered columnstore index. The index is ordered on SHIPDATE.

```sql
CREATE TABLE Lineitem  
WITH (DISTRIBUTION = ROUND_ROBIN, CLUSTERED COLUMNSTORE INDEX ORDER(SHIPDATE))  
AS  
SELECT * FROM ext_Lineitem
```

## <a id="ExTableDistribution"></a> Examples for table distribution

### <a id="RoundRobin"></a> F. Create a ROUND_ROBIN table
 The following example creates a ROUND_ROBIN table with three columns and without partitions. The data is spread across all distributions. The table is created with a CLUSTERED COLUMNSTORE INDEX, which gives better performance and data compression than a heap or rowstore clustered index.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a id="HashDistributed"></a> G. Create a table that's hash-distributed on multiple columns (preview)

The following example creates the same table as the previous example. However, for this table, rows are distributed (on `id` and `zipCode` columns). The table is created with a clustered columnstore index, which gives better performance and data compression than a heap or rowstore clustered index.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id, zipCode), 
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a id="Replicated"></a> H. Create a replicated table
 The following example creates a replicated table similar to the previous examples. Replicated tables are copied in full to each Compute node. With this copy on each Compute node, data movement is reduced for queries. This example is created with a CLUSTERED INDEX, which gives better data compression than a heap. A heap may not contain enough rows to achieve good CLUSTERED COLUMNSTORE INDEX compression.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,
    CLUSTERED INDEX (lastName)  
  );  
```  

## <a id="ExTablePartitions"></a> Examples for table partitions

### <a id="PartitionedTable"></a> I. Create a partitioned table

 The following example creates the same table as shown in example A, with the addition of RANGE LEFT partitioning on the `id` column. It specifies four partition boundary values, which results in five partitions.  
  
```sql
CREATE TABLE myTable
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
  (
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX
  );  
```  
  
 In this example, data will be sorted into the following partitions:  
  
- Partition 1: col <= 10
- Partition 2: 10 < col <= 20
- Partition 3: 20 < col <= 30
- Partition 4: 30 < col <= 40
- Partition 5: 40 < col  
  
 If this same table was partitioned RANGE RIGHT instead of RANGE LEFT (default), the data will be sorted into the following partitions:  
  
- Partition 1: col < 10  
- Partition 2: 10 <= col < 20
- Partition 3: 20 <= col < 30
- Partition 4: 30 <= col < 40
- Partition 5: 40 <= col  
  
### <a id="OnePartition"></a> J. Create a partitioned table with one partition

 The following example creates a partitioned table with one partition. It doesn't specify any boundary value, which results in one partition.  
  
```sql
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH
    (
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a id="DatePartition"></a> K. Create a table with date partitioning

 The following example creates a new table named `myTable`, with partitioning on a `date` column. By using RANGE RIGHT and dates for the boundary values, it puts a month of data in each partition.  
  
```sql
CREATE TABLE myTable (  
    l_orderkey      bigint,
    l_partkey       bigint,
    l_suppkey       bigint,
    l_linenumber    bigint,
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH
  (
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
## Next steps
 
- [CREATE TABLE AS SELECT (Azure Synapse Analytics)](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
- [DROP TABLE (Transact-SQL)](../../t-sql/statements/drop-table-transact-sql.md)
- [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)
- [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)

::: moniker-end
::: moniker range="=fabric"

[!INCLUDE[applies-to-version/fabric-dw-only](../../includes/applies-to-version/fabric-dw.md)]

 Creates a new table in a [!INCLUDE[fabric-data-warehouse](../../includes/fabric-dw.md)] in [!INCLUDE[microsoft-fabric](../../includes/fabric.md)].  

 For more information, see [Create tables on [!INCLUDE[fabric-data-warehouse](../../includes/fabric-dw.md)] in [!INCLUDE[microsoft-fabric](../../includes/fabric.md)]](/fabric/data-warehouse/create-table).

> [!NOTE]
> For reference to [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], visit [CREATE TABLE (Azure Synapse Analytics)](create-table-azure-sql-data-warehouse.md?view=azure-sqldw-latest&preserve-view=true).
> For SQL Server and Azure SQL platforms, visit [CREATE TABLE](create-table-transact-sql.md?view=azuresqldb-current&preserve-view=true) and select your desired product version from the version drop down list.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a id="Syntax"></a> Syntax

```syntaxsql
-- Create a new table.
CREATE TABLE { database_name.schema_name.table_name | schema_name.table_name | table_name }
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]
    )  
[;]  

<column_options> ::=
    [ NULL | NOT NULL ] -- default is NULL

<data type> ::=
      datetime2 ( n )   
    | date  
    | time ( n )   
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | bigint  
    | int   
    | smallint  
    | bit  
    | varchar [ ( n ) ] 
    | char [ ( n ) ]  
    | varbinary [ ( n ) ] 
    | binary [ ( n ) ]  
    | uniqueidentifier  
```

## Arguments

#### *database_name*
 The name of the database that will contain the new table. The default is the current database.  
  
#### *schema_name*
 The schema for the table. Specifying *schema* is optional. If blank, the default schema is used.  
  
#### *table_name*
 The name of the new table. To create a local temporary table, precede the table name with `#`.

#### *column_name*
 The name of a table column.

### <a id="ColumnOptions"></a> Column options

 `NULL` | `NOT NULL`  
 Specifies whether `NULL` values are allowed in the column. The default is `NULL`.  
  
### <a id="DataTypesFabric"></a> Data type

[!INCLUDE [fabric](../../includes/fabric.md)] supports the most commonly used data types. 

> [!NOTE]
> Similar to SQL Server, there is an 8060 byte per row limit. This may become a blocking issue for tables that have many columns, or columns with large data types, such as `varchar(8000)` or `varbinary(8000)`. Inserts or updates that violate the 8060 byte limit will result in error codes 511 or 611. For more information, see [Pages and Extents Architecture Guide](../../relational-databases/pages-and-extents-architecture-guide.md?view=azure-sqldw-latest&preserve-view=true#row-overflow-considerations).

For a table of data type conversions, see the Implicit Conversions section of [CAST and CONVERT (Transact-SQL)](../functions/cast-and-convert-transact-sql.md). For more information, see [Date and Time Data Types and Functions (Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md).

The following list of supported data types includes their details and storage bytes. 

 `datetime2` ( *n* )   
Stores date and time of day with 19 to 26 characters according to the Gregorian calendar. The date can contain year, month, and day. The time contains hour, minutes, seconds. As an option, you can store and display zero to six digits for fractional seconds based on the *n* parameter. The storage size is 8 bytes. *n* must be a value from `0` to `6`.

> [!NOTE]
> There is no default precision like other SQL platforms.  You must provide the value for precision from `0` to `6`.

  
|*n* value|Precision|Scale|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
  
 `date`  
 Stores a date using a maximum of 10 characters for year, month, and day according to the Gregorian calendar. The storage size is 3 bytes. Date is stored as an integer.  
  
 `time` ( *n* )   
 *n* must be a value from `0` to `6`.
  
 `float` [ ( *n* ) ]  
 Approximate number data type for use with floating point numeric data. Floating point data is approximate, which means that not all values in the data type range can be represented exactly. *n* specifies the number of bits used to store the mantissa of the `float` in scientific notation. *n* dictates the precision and storage size. If *n* is specified, it must be a value between `1` and `53`. The default value of *n* is `53`.  
  
> [!NOTE]
> There is no default precision like other SQL platforms.  You must provide the value for precision from `0` to `6`.


| *n* value | Precision | Storage size |  
| --------: | --------: | -----------: |  
| 1-24   | 7 digits  | 4 bytes      |  
| 25-53  | 15 digits | 8 bytes      |  
  
 [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] treats *n* as one of two possible values. If `1`<= *n* <= `24`, *n* is treated as `24`. If `25` <= *n* <= `53`, *n* is treated as `53`.  
  
 The [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] `float` data type complies with the ISO standard for all values of *n* from `1` through `53`. The synonym for double precision is `float(53)`.  
  
 `real` [ ( *n* ) ]  
 The definition of real is the same as float. The ISO synonym for `real` is `float(24)`.  
  
 `decimal` [ ( *precision* [ *, scale* ] ) ] | `numeric` [ ( *precision* [ *, scale* ] ) ]  
 Stores fixed precision and scale numbers.  
  
 *precision*  
 The maximum total number of decimal digits that can be stored, both to the left and to the right of the decimal point. The precision must be a value from `1` through the maximum precision of `38`. The default precision is `18`.  
  
 *scale*  
 The maximum number of decimal digits that can be stored to the right of the decimal point. *Scale* must be a value from `0` through *precision*. You can only specify *scale* if *precision* is specified. The default scale is `0` and so `0` <= *scale* <= *precision*. Maximum storage sizes vary, based on the precision.  
  
| Precision | Storage bytes  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `bigint` \| `int` \| `smallint`  
 Exact-number data types that use integer data. The storage is shown in the following table.  
  
| Data Type | Storage bytes |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
  
 `bit`  
 An integer data type that can take the value of `1`, `0`, or `NULL. [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] optimizes storage of bit columns. If there are 8 or fewer bit columns in a table, the columns are stored as 1 byte. If there are from 9-16 bit columns, the columns are stored as 2 bytes, and so on.  
  
 `varchar` [ ( *n* ) ]
 Variable-length, Unicode character data with a length of *n* bytes. *n* must be a value from `1` to `8000`. The storage size is the actual length of data entered + 2 bytes. The default for *n* is `1`.   
  
 `char` [ ( *n* ) ]  
 Fixed-length, Unicode character data with a length of *n* bytes. *n* must be a value from `1` to `8000`. The storage size is *n* bytes. The default for *n* is `1`.  
  
 `varbinary` [ ( *n* ) ] 
 Variable-length binary data. *n* can be a value from `1` to `8000`. The storage size is the actual length of data entered + 2 bytes. The default value for *n* is 7.  
  
 `uniqueidentifier`  
 Is a 16-byte GUID. 

## Permissions

Permissions in [!INCLUDE[fabric](../../includes/fabric.md)] are different from permissions [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].

## <a id="LimitationsRestrictions"></a> Limitations and restrictions

- Table names cannot be greater than 128 characters.
- Table names in [!INCLUDE [fabricdw](../../includes/fabric-dw.md)] in [!INCLUDE [fabric](../../includes/fabric.md)] cannot include the characters `/` or `\`.
- Column names cannot be greater than 128 characters.
- The default and only collation supported in [!INCLUDE [fabricdw](../../includes/fabric-dw.md)] is Latin1_General_100_BIN2_UTF8.

## Remarks

There is limited TSQL functionality in [!INCLUDE [fabricdw](../../includes/fabric-dw.md)]. For more information, see [TSQL Surface Area in [!INCLUDE[fabric](../../includes/fabric.md)]](/fabric/data-warehouse/tsql-surface-area).

## <a id="LockingBehavior"></a> Locking behavior
 Takes a Schema-Modification lock on the table, a shared lock on the DATABASE, and a Schema-Stability lock on the SCHEMA.  

## Next steps

- [Create tables on [!INCLUDE[fabric-data-warehouse](../../includes/fabric-dw.md)] in [!INCLUDE[microsoft-fabric](../../includes/fabric.md)]](/fabric/data-warehouse/create-table)
- [What is data warehousing in [!INCLUDE [fabric](../../includes/fabric.md)]?](/fabric/data-warehouse/data-warehousing)

::: moniker-end
