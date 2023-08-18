---
title: "BULK INSERT (Transact-SQL)"
description: Transact-SQL reference for the BULK INSERT statement.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 05/12/2022
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "BULK_TSQL"
  - "BULK_INSERT"
  - "BULK_INSERT_TSQL"
  - "BULK INSERT"
helpviewer_keywords:
  - "tables [SQL Server], importing data into"
  - "inserting files"
  - "views [SQL Server], importing data into"
  - "BULK INSERT statement"
  - "views [SQL Server], exporting data from"
  - "importing data, bulk import"
  - "bulk importing [SQL Server], BULK INSERT statement"
  - "file importing [SQL Server]"
dev_langs:
  - "TSQL"
---
# BULK INSERT (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Imports a data file into a database table or view in a user-specified format in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
BULK INSERT
   { database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }
      FROM 'data_file'
     [ WITH
    (
   [ [ , ] BATCHSIZE = batch_size ]
   [ [ , ] CHECK_CONSTRAINTS ]
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]
   [ [ , ] DATAFILETYPE =
      { 'char' | 'native' | 'widechar' | 'widenative' } ]
   [ [ , ] DATA_SOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATA_SOURCE = 'errorfile_data_source_name' ]
   [ [ , ] FIRSTROW = first_row ]
   [ [ , ] FIRE_TRIGGERS ]
   [ [ , ] FORMATFILE_DATA_SOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]
   [ [ , ] KEEPNULLS ]
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]
   [ [ , ] LASTROW = last_row ]
   [ [ , ] MAXERRORS = max_errors ]
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
   [ [ , ] TABLOCK ]

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]
    )]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *database_name*

The database name in which the specified table or view resides. If not specified, *database_name* is the current database.

#### *schema_name*

Specifies the name of the table or view schema. *schema_name* is optional if the default schema for the user performing the bulk-import operation is schema of the specified table or view. If *schema* isn't specified and the default schema of the user performing the bulk-import operation is different from the specified table or view, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] returns an error message, and the bulk-import operation is canceled.

#### *table_name*

Specifies the name of the table or view to bulk import data into. Only views in which all columns refer to the same base table can be used. For more information about the restrictions for loading data into views, see [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).

#### FROM '*data_file*'

Specifies the full path of the data file that contains data to import into the specified table or view. BULK INSERT can import data from a disk or Azure Blob Storage (including network, floppy disk, hard disk, and so on).

*data_file* must specify a valid path from the server on which [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is running. If *data_file* is a remote file, specify the Universal Naming Convention (UNC) name. A UNC name has the form `\\SystemName\ShareName\Path\FileName`. For example:

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.dat';
```

Beginning with [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)], the *data_file* can be in Azure Blob Storage. In that case, you need to specify **data_source_name** option. For an example, see [Import data from a file in Azure Blob Storage](#f-import-data-from-a-file-in-azure-blob-storage).

Azure SQL Database only supports reading from Azure Blob Storage.

#### BATCHSIZE = *batch_size*

Specifies the number of rows in a batch. Each batch is copied to the server as one transaction. If this fails, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] commits or rolls back the transaction for every batch. By default, all data in the specified data file is one batch. For information about performance considerations, see [Performance considerations](#performance-considerations) later in this article.

#### CHECK_CONSTRAINTS

Specifies that all constraints on the target table or view must be checked during the bulk-import operation. Without the CHECK_CONSTRAINTS option, any CHECK and FOREIGN KEY constraints are ignored, and after the operation, the constraint on the table is marked as not-trusted.

UNIQUE and PRIMARY KEY constraints are always enforced. When importing into a character column that is defined with a NOT NULL constraint, BULK INSERT inserts a blank string when there's no value in the text file.

At some point, you must examine the constraints on the whole table. If the table was non-empty before the bulk-import operation, the cost of revalidating the constraint may exceed the cost of applying CHECK constraints to the incremental data.

A situation in which you might want constraints disabled (the default behavior) is if the input data contains rows that violate constraints. With CHECK constraints disabled, you can import the data and then use [!INCLUDE[tsql](../../includes/tsql-md.md)] statements to remove the invalid data.

> [!NOTE]  
> The MAXERRORS option does not apply to constraint checking.

#### CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | '*code_page*' }

Specifies the code page of the data in the data file. CODEPAGE is relevant only if the data contains **char**, **varchar**, or **text** columns with character values greater than **127** or less than **32**. For an example, see [Specify a code page](#d-specify-a-code-page).

CODEPAGE isn't a supported option on Linux for [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)]. For [!INCLUDE[sssql19-md](../../includes/sssql19-md.md)], only the **'RAW'** option is allowed for CODEPAGE.

You should specify a collation name for each column in a [format file](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).

|CODEPAGE value|Description|
|--------------------|-----------------|
|ACP|Columns of **char**, **varchar**, or **text** data type are converted from the [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows code page (ISO 1252) to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] code page.|
|OEM (default)|Columns of **char**, **varchar**, or **text** data type are converted from the system OEM code page to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] code page.|
|RAW|No conversion from one code page to another occurs. RAW is the fastest option.|
|*code_page*|Specific code page number, for example, 850.<br /><br />Versions prior to [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] don't support code page 65001 (UTF-8 encoding).|

#### DATAFILETYPE = { 'char' | 'native' | 'widechar' | 'widenative' }

Specifies that BULK INSERT performs the import operation using the specified data-file type value.

|DATAFILETYPE value|All data represented in:|
|------------------------|------------------------------|
|**char** (default)|Character format.<br /><br />For more information, see [Use Character Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|
|**native**|Native (database) data types. Create the native data file by bulk importing data from [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using the **bcp** utility.<br /><br />The native value offers a higher performance alternative to the char value. Native format is recommended when you bulk transfer data between multiple instances of SQL Server using a data file that doesn't contain any extended/double-byte character set (DBCS) characters.<br /><br />For more information, see [Use Native Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|
|**widechar**|Unicode characters.<br /><br />For more information, see [Use Unicode Character Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|
|**widenative**|Native (database) data types, except in **char**, **varchar**, and **text** columns, in which data is stored as Unicode. Create the **widenative** data file by bulk importing data from [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using the **bcp** utility.<br /><br />The **widenative** value offers a higher performance alternative to **widechar**. If the data file contains [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] extended characters, specify **widenative**.<br /><br />For more information, see [Use Unicode Native Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|

#### DATA_SOURCE = '*data_source_name*'

**Applies to:** [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)] and Azure SQL Database.

Specifies a named external data source pointing to the Azure Blob Storage location of the file that will be imported. The external data source must be created using the `TYPE = BLOB_STORAGE` option added in [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)]. For more information, see [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). For an example, see [Import data from a file in Azure Blob Storage](#f-import-data-from-a-file-in-azure-blob-storage).

#### ERRORFILE = '*error_file_path*'

Specifies the file used to collect rows that have formatting errors and can't be converted to an OLE DB rowset. These rows are copied into this error file from the data file "as is."

The error file is created when the command is executed. An error occurs if the file already exists. Additionally, a control file that has the extension `.ERROR.txt` is created, which references each row in the error file and provides error diagnostics. As soon as the errors have been corrected, the data can be loaded.

Beginning with [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)], the *error_file_path* can be in Azure Blob Storage.

#### ERRORFILE_DATA_SOURCE = '*errorfile_data_source_name*'

**Applies to:** [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)].

Specifies a named external data source pointing to the Azure Blob Storage location of the error file that will contain errors found during the import. The external data source must be created using the `TYPE = BLOB_STORAGE` option added in [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)]. For more information, see [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

#### FIRSTROW = *first_row*

Specifies the number of the first row to load. The default is the first row in the specified data file. FIRSTROW is 1-based.

The FIRSTROW attribute isn't intended to skip column headers. Skipping headers isn't supported by the BULK INSERT statement. If you choose to skip rows, the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] looks only at the field terminators, and doesn't validate the data in the fields of skipped rows.

#### FIRE_TRIGGERS

Specifies that any insert triggers defined on the destination table execute during the bulk-import operation. If triggers are defined for INSERT operations on the target table, they're fired for every completed batch.

If FIRE_TRIGGERS isn't specified, no insert triggers execute.

#### FORMATFILE_DATA_SOURCE = '*data_source_name*'

**Applies to:** [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)].

Specifies a named external data source pointing to the Azure Blob Storage location of the format file that will define the schema of imported data. The external data source must be created using the `TYPE = BLOB_STORAGE` option added in [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)]. For more information, see [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

#### KEEPIDENTITY

Specifies that identity value or values in the imported data file are to be used for the identity column. If KEEPIDENTITY isn't specified, the identity values for this column are verified but not imported and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatically assigns unique values based on the seed and increment values specified during table creation. If the data file doesn't contain values for the identity column in the table or view, use a format file to specify that the identity column in the table or view is to be skipped when importing data; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatically assigns unique values for the column. For more information, see [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).

For more information, see about keeping identify values see [Keep Identity Values When Bulk Importing Data &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).

#### KEEPNULLS

Specifies that empty columns should retain a null value during the bulk-import operation, instead of having any default values for the columns inserted. For more information, see [Keep Nulls or Use Default Values During Bulk Import &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).

#### KILOBYTES_PER_BATCH = *kilobytes_per_batch*

Specifies the approximate number of kilobytes (KB) of data per batch as *kilobytes_per_batch*. By default, KILOBYTES_PER_BATCH is unknown. For information about performance considerations, see [Performance considerations](#performance-considerations) later in this article.

#### LASTROW = *last_row*

Specifies the number of the last row to load. The default is 0, which indicates the last row in the specified data file.

#### MAXERRORS = *max_errors*

Specifies the maximum number of syntax errors allowed in the data before the bulk-import operation is canceled. Each row that can't be imported by the bulk-import operation is ignored and counted as one error. If *max_errors* isn't specified, the default is 10.

The MAX_ERRORS option doesn't apply to constraint checks or to converting **money** and **bigint** data types.

#### ORDER ( { *column* [ ASC | DESC ] } [ ,... *n* ] )

Specifies how the data in the data file is sorted. Bulk import performance is improved if the data being imported is sorted according to the clustered index on the table, if any. If the data file is sorted in a different order, that is other than the order of a clustered index key or if there's no clustered index on the table, the ORDER clause is ignored. The column names supplied must be valid column names in the destination table. By default, the bulk insert operation assumes the data file is unordered. For optimized bulk import, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] also validates that the imported data is sorted.

*n* is a placeholder that indicates that multiple columns can be specified.

#### ROWS_PER_BATCH = *rows_per_batch*

Indicates the approximate number of rows of data in the data file.

By default, all the data in the data file is sent to the server as a single transaction, and the number of rows in the batch is unknown to the query optimizer. If you specify ROWS_PER_BATCH (with a value > 0) the server uses this value to optimize the bulk-import operation. The value specified for ROWS_PER_BATCH should approximately the same as the actual number of rows. For information about performance considerations, see [Performance considerations](#performance-considerations) later in this article.

#### TABLOCK

Specifies that a table-level lock is acquired for the duration of the bulk-import operation. A table can be loaded concurrently by multiple clients if the table has no indexes and TABLOCK is specified. By default, locking behavior is determined by the table option **table lock on bulk load**. Holding a lock for the duration of the bulk-import operation reduces lock contention on the table, in some cases can significantly improve performance. For information about performance considerations, see [Performance considerations](#performance-considerations) later in this article.

For a columnstore index, the locking behavior is different because it's internally divided into multiple rowsets. Each thread loads data exclusively into each rowset by taking an X lock on the rowset allowing parallel data load with concurrent data load sessions. The use of TABLOCK option will cause thread to take an X lock on the table (unlike BU lock for traditional rowsets) which will prevent other concurrent threads to load data concurrently.

### Input file format options

#### FORMAT = 'CSV'

**Applies to:** [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)].

Specifies a comma-separated values file compliant to the [RFC 4180](https://tools.ietf.org/html/rfc4180) standard.

```sql
BULK INSERT Sales.Orders
FROM '\\SystemX\DiskZ\Sales\data\orders.csv'
WITH ( FORMAT = 'CSV');
```

#### FIELDQUOTE = '*field_quote*'

**Applies to:** [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)].

Specifies a character that will be used as the quote character in the CSV file. If not specified, the quote character (") will be used as the quote character as defined in the [RFC 4180](https://tools.ietf.org/html/rfc4180) standard.

#### FORMATFILE = '*format_file_path*'

Specifies the full path of a format file. A format file describes the data file that contains stored responses created by using the **bcp** utility on the same table or view. The format file should be used if:

- The data file contains greater or fewer columns than the table or view.
- The columns are in a different order.
- The column delimiters vary.
- There are other changes in the data format. Format files are typically created by using the **bcp** utility and modified with a text editor as needed. For more information, see [bcp Utility](../../tools/bcp-utility.md) and [Create a format file](../../relational-databases/import-export/create-a-format-file-sql-server.md).

Beginning with [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)], and in Azure SQL Database, `format_file_path` can be in Azure Blob Storage.

#### FIELDTERMINATOR = '*field_terminator*'

Specifies the field terminator to be used for **char** and **widechar** data files. The default field terminator is `\t` (tab character). For more information, see [Specify Field and Row Terminators &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).

#### ROWTERMINATOR = '*row_terminator*'

Specifies the row terminator to be used for **char** and **widechar** data files. The default row terminator is `\r\n` (newline character). For more information, see [Specify Field and Row Terminators &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).

## Compatibility

BULK INSERT enforces strict data validation and data checks of data read from a file that could cause existing scripts to fail when they're executed on invalid data. For example, BULK INSERT verifies that:

- The native representations of **float** or **real** data types are valid.
- Unicode data has an even-byte length.

## Data types

### String-to-decimal data type conversions

The string-to-decimal data type conversions used in BULK INSERT follow the same rules as the [!INCLUDE[tsql](../../includes/tsql-md.md)] [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) function, which rejects strings representing numeric values that use scientific notation. Therefore, BULK INSERT treats such strings as invalid values and reports conversion errors.

To work around this behavior, use a format file to bulk import scientific notation **float** data into a decimal column. In the format file, explicitly describe the column as **real** or **float** data. For more information about these data types, see [float and real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).

Format files represent **real** data as the **SQLFLT4** data type and **float** data as the **SQLFLT8** data type. For information about non-XML format files, see [Specify File Storage Type by Using bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).

#### Example of importing a numeric value that uses scientific notation

This example uses the following table in the `bulktest` database:

```sql
CREATE TABLE dbo.t_float(c1 FLOAT, c2 DECIMAL (5,4));
```

The user wants to bulk import data into the `t_float` table. The data file, C:\t_float-c.dat, contains scientific notation **float** data; for example:

```input
8.0000000000000002E-2 8.0000000000000002E-2
```

When copying this sample, be aware of different text editors and encodings that save tabs characters (\t) as spaces. A tab character is expected later in this sample.

However, BULK INSERT can't import this data directly into `t_float`, because its second column, `c2`, uses the `decimal` data type. Therefore, a format file is necessary. The format file must map the scientific notation **float** data to the decimal format of column `c2`.

The following format file uses the `SQLFLT8` data type to map the second data field to the second column:

```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<RECORD>
<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/>
<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/> </RECORD> <ROW>
<COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/>
<COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/> </ROW> </BCPFORMAT>
```

To use this format file (using the file name `C:\t_floatformat-c-xml.xml`) to import the test data into the test table, issue the following [!INCLUDE[tsql](../../includes/tsql-md.md)] statement:

```sql
BULK INSERT bulktest.dbo.t_float
FROM 'C:\t_float-c.dat' WITH (FORMATFILE = 'C:\t_floatformat-c-xml.xml');
```

> [!IMPORTANT]  
> Azure SQL Database only supports reading from Azure Blob Storage.

### Data types for bulk exporting or importing SQLXML documents

To bulk export or import SQLXML data, use one of the following data types in your format file:

|Data type|Effect|
|---------------|------------|
|SQLCHAR or SQLVARCHAR|The data is sent in the client code page or in the code page implied by the collation). The effect is the same as specifying the DATAFILETYPE **= 'char'** without specifying a format file.|
|SQLNCHAR or SQLNVARCHAR|The data is sent as Unicode. The effect is the same as specifying the DATAFILETYPE **= 'widechar'** without specifying a format file.|
|SQLBINARY or SQLVARBIN|The data is sent without any conversion.|

## Remarks

For a comparison of the BULK INSERT statement, the INSERT ... SELECT \* FROM OPENROWSET(BULK...) statement, and the **bcp** command, see [Bulk Import and Export of Data &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).

For information about preparing data for bulk import, see [Prepare Data for Bulk Export or Import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

The BULK INSERT statement can be executed within a user-defined transaction to import data into a table or view. Optionally, to use multiple matches for bulk importing data, a transaction can specify the BATCHSIZE clause in the BULK INSERT statement. If a multiple-batch transaction is rolled back, every batch that the transaction has sent to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is rolled back.

## Interoperability

### Import data from a CSV file

Beginning with [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)], BULK INSERT supports the CSV format, as does Azure SQL Database.

Before [!INCLUDE [sssql17-md](../../includes/sssql17-md.md)], comma-separated value (CSV) files aren't supported by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bulk-import operations. However, in some cases, a CSV file can be used as the data file for a bulk import of data into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For information about the requirements for importing data from a CSV data file, see [Prepare Data for Bulk Export or Import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

## Log behavior

For information about when row-insert operations that are performed by bulk import into SQL Server are logged in the transaction log, see [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md). Minimal logging isn't supported in Azure SQL Database.

## Restrictions

When using a format file with BULK INSERT, you can specify up to 1024 fields only. This is same as the maximum number of columns allowed in a table. If you use a format file with BULK INSERT with a data file that contains more than 1024 fields, BULK INSERT generates the 4822 error. The [bcp utility](../../tools/bcp-utility.md) doesn't have this limitation, so for data files that contain more than 1024 fields, use BULK INSERT without a format file or use the **bcp** command.

## Performance considerations

If the number of pages to be flushed in a single batch exceeds an internal threshold, a full scan of the buffer pool might occur to identify which pages to flush when the batch commits. This full scan can hurt bulk-import performance. A likely case of exceeding the internal threshold occurs when a large buffer pool is combined with a slow I/O subsystem. To avoid buffer overflows on large machines, either don't use the TABLOCK hint (which will remove the bulk optimizations) or use a smaller batch size (which preserves the bulk optimizations).

You should test various batch sizes with your data load to find out what works best for you. Keep in mind that the batch size has partial rollback implications. If your process fails and before you use BULK INSERT again, you may have to do additional manual work to remove a part of the rows that were inserted successfully, before a failure occurred.

With Azure SQL Database, consider temporarily increasing the performance level of the database or instance prior to the import if you're importing a large volume of data.

## Security

### Security account delegation (impersonation)

If a user uses a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login, the security profile of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] process account is used. A login using SQL Server authentication can't be authenticated outside of the Database Engine. Therefore, when a BULK INSERT command is initiated by a login using SQL Server authentication, the connection to the data is made using the security context of the SQL Server process account (the account used by the SQL Server Database Engine service).

To successfully read the source data you must grant the account used by the SQL Server Database Engine, access to the source data. In contrast, if a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] user logs on by using Windows Authentication, the user can read only those files that can be accessed by the user account, regardless of the security profile of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] process.

When executing the BULK INSERT statement by using **sqlcmd** or **osql**, from one computer, inserting data into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on a second computer, and specifying a *data_file* on third computer by using a UNC path, you may receive a 4861 error.

To resolve this error, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication and specify a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login that uses the security profile of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] process account, or configure Windows to enable security account delegation. For information about how to enable a user account to be trusted for delegation, see Windows Help.

For more information about this and other security considerations for using BULK INSERT, see [Import Bulk Data by Using BULK INSERT or OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

When importing from Azure Blob Storage and the data isn't public (anonymous access), create a [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) based on a SAS key encrypted with a [MASTER KEY](create-master-key-transact-sql.md), and then create an [external database source](../../t-sql/statements/create-external-data-source-transact-sql.md) for use in your BULK INSERT command. 

Alternatively, create a [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) based on `MANAGED IDENTITY` to authorize requests for data access in non-public storage accounts. When using `MANAGED IDENTITY`, Azure storage must grant permissions to the managed identity of the instance by adding the **Storage Blob Data Contributor** built-in Azure role-based access control (RBAC) role that provides read/write access to the managed identity for the necessary Azure Blob Storage containers. Azure SQL Managed Instance have a system assigned managed identity, and can also have one or more user-assigned managed identities. You can use either system-assigned managed identities or user-assigned managed identities to authorize the requests. For authorization, the `default` identity of the managed instance would be used (that is primary user-assigned managed identity, or system-assigned managed identity if user-assigned managed identity is not specified). For an example, see [Import data from a file in Azure Blob Storage](#f-import-data-from-a-file-in-azure-blob-storage).


> [!IMPORTANT]
> Managed Identity is applicable only to Azure SQL. SQL Server does not support Managed Identity.

### Permissions

Requires INSERT and ADMINISTER BULK OPERATIONS permissions. In Azure SQL Database, INSERT and ADMINISTER DATABASE BULK OPERATIONS permissions are required. ADMINISTER BULK OPERATIONS permissions or the **bulkadmin** role isn't supported for SQL Server on Linux. Only the **sysadmin** can perform bulk inserts for SQL Server on Linux.

Additionally, ALTER TABLE permission is required if one or more of the following conditions is true:

- Constraints exist and the CHECK_CONSTRAINTS option isn't specified.

  Disabling constraints is the default behavior. To check constraints explicitly, use the CHECK_CONSTRAINTS option.

- Triggers exist and the FIRE_TRIGGER option isn't specified.

  By default, triggers aren't fired. To fire triggers explicitly, use the FIRE_TRIGGER option.

- You use the KEEPIDENTITY option to import identity value from data file.

## Examples

### A. Use pipes to import data from a file

The following example imports order detail information into the `AdventureWorks2022.Sales.SalesOrderDetail` table from the specified data file by using a pipe (`|`) as the field terminator and `|\n` as the row terminator.

```sql
BULK INSERT AdventureWorks2022.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
      (
         FIELDTERMINATOR = ' |'
         , ROWTERMINATOR = ' |\n'
      );
```

> [!IMPORTANT]
>
> Azure SQL Database only supports reading from Azure Blob Storage.

### B. Use the FIRE_TRIGGERS argument

The following example specifies the `FIRE_TRIGGERS` argument.

```sql
BULK INSERT AdventureWorks2022.Sales.SalesOrderDetail
   FROM 'f:\orders\lineitem.tbl'
   WITH
     (
         FIELDTERMINATOR = ' |'
         , ROWTERMINATOR = ':\n'
         , FIRE_TRIGGERS
      );
```

> [!IMPORTANT]
> Azure SQL Database only supports reading from Azure Blob Storage.

### C. Use line feed as a row terminator

The following example imports a file that uses the line feed as a row terminator such as a UNIX output:

```sql
DECLARE @bulk_cmd VARCHAR(1000);
SET @bulk_cmd = 'BULK INSERT AdventureWorks2022.Sales.SalesOrderDetail
FROM ''<drive>:\<path>\<filename>''
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';
EXEC(@bulk_cmd);
```

> [!NOTE]  
> Owing to the way Microsoft Windows treats text files, `\n` is automatically replaced with `\r\n`.

> [!IMPORTANT]  
> Azure SQL Database only supports reading from Azure Blob Storage.

### D. Specify a code page

The following example shows how to specify a code page.

```sql
BULK INSERT MyTable
FROM 'D:\data.csv'
WITH
( CODEPAGE = '65001'
   , DATAFILETYPE = 'char'
   , FIELDTERMINATOR = ','
);
```

> [!IMPORTANT]
> Azure SQL Database only supports reading from Azure Blob Storage.

### E. Import data from a CSV file

The following example shows how to specify a CSV file, skipping the header (first row), using `;` as field terminator and `0x0a` as line terminator:

```sql
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'
      , FIRSTROW = 2
      , FIELDQUOTE = '\'
      , FIELDTERMINATOR = ';'
      , ROWTERMINATOR = '0x0a');
```

The following example shows how to specify a CSV file in UTF-8 format (using a `CODEPAGE` of `65001`), skipping the header (first row), using `;` as field terminator and `0x0a` as line terminator:

```sql
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH ( CODEPAGE = '65001'
      , FORMAT = 'CSV'
      , FIRSTROW = 2
      , FIELDQUOTE = '\'
      , FIELDTERMINATOR = ';'
      , ROWTERMINATOR = '0x0a');
```

> [!IMPORTANT]
> Azure SQL Database only supports reading from Azure Blob Storage.

### F. Import data from a file in Azure Blob Storage

The following example shows how to load data from a CSV file in an Azure Blob Storage location on which you've created a Shared Access Signature (SAS). The Azure Blob Storage location is configured as an external data source, which requires a database scoped credential using a SAS key that is encrypted using a master key in the user database.

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

-- NOTE: Make sure that you don't have a leading ? in SAS token, and
-- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
-- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL = MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

The following example shows how to use the BULK INSERT command to load data from a csv file in an Azure Blob storage location using Managed Identity. The Azure Blob storage location is configured as an external data source. 

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential 
WITH IDENTITY = 'Managed Identity';
-- NOTE: Make sure you have granted Storage Bob Data Contributor RBAC on storage to provides read/write access to the managed identity for the necessary Azure Blob Storage containers.
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);
BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Managed Identity is applicable only to Azure SQL. SQL Server does not support Managed Identity.

> [!IMPORTANT]
> Azure SQL only supports reading from Azure Blob Storage.

### G. Import data from a file in Azure Blob Storage and specify an error file

The following example shows how to load data from a CSV file in an Azure Blob Storage location, which has been configured as an external data source, and also specifying an error file. You will need a database scoped credential using a shared access signature. If running on Azure SQL Database, ERRORFILE option should be accompanied by ERRORFILE_DATA_SOURCE otherwise the import might fail with permissions error. The file specified in ERRORFILE shouldn't exist in the container.

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (
         DATA_SOURCE = 'MyAzureInvoices'
         , FORMAT = 'CSV'
         , ERRORFILE = 'MyErrorFile'
         , ERRORFILE_DATA_SOURCE = 'MyAzureInvoices');
```

For complete `BULK INSERT` examples including configuring the credential and external data source, see [Examples of Bulk Access to Data in Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

### More examples

Other `BULK INSERT` examples are provided in the following articles:

- [Examples of Bulk Import and Export of XML Documents &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [Keep Identity Values When Bulk Importing Data &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [Keep Nulls or Use Default Values During Bulk Import &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [Specify Field and Row Terminators &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)
- [Use a Format File to Bulk Import Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [Use Character Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [Use Native Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)
- [Use Unicode Character Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
- [Use Unicode Native Format to Import or Export Data &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)
- [Use a Format File to Skip a Table Column &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [Use a Format File to Map Table Columns to Data-File Fields &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## See also

- [Bulk Import and Export of Data &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [bcp Utility](../../tools/bcp-utility.md)
- [Format Files for Importing or Exporting Data &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [Prepare Data for Bulk Export or Import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)
- [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)
