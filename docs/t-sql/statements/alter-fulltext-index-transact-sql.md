---
title: "ALTER FULLTEXT INDEX (Transact-SQL)"
description: Changes the properties of a full-text index in SQL Server and Azure SQL.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 07/28/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ALTER FULLTEXT INDEX"
  - "ALTER_FULLTEXT_INDEX_TSQL"
helpviewer_keywords:
  - "full-text search [SQL Server], search property lists"
  - "modifying full-text indexes"
  - "full-text indexes [SQL Server], modifying"
  - "search property lists [SQL Server], associating with full-text indexes"
  - "ALTER FULLTEXT INDEX statement"
dev_langs:
  - "TSQL"
---
# ALTER FULLTEXT INDEX (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Changes the properties of a full-text index in [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
ALTER FULLTEXT INDEX ON table_name
   { ENABLE
   | DISABLE
   | SET CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF }
   | ADD ( column_name
           [ TYPE COLUMN type_column_name ]
           [ LANGUAGE language_term ]
           [ STATISTICAL_SEMANTICS ]
           [ , ...n ]
         )
     [ WITH NO POPULATION ]
   | ALTER COLUMN column_name
     { ADD | DROP } STATISTICAL_SEMANTICS
     [ WITH NO POPULATION ]
   | DROP ( column_name [ , ...n ] )
     [ WITH NO POPULATION ]
   | START { FULL | INCREMENTAL | UPDATE } POPULATION
   | { STOP | PAUSE | RESUME } POPULATION
   | SET STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }
     [ WITH NO POPULATION ]
   | SET SEARCH PROPERTY LIST [ = ] { OFF | property_list_name }
     [ WITH NO POPULATION ]
   }
[ ; ]
```

[!INCLUDE [sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *table_name*

The name of the table or indexed view that contains the column or columns included in the full-text index. Specifying database and table owner names is optional.

#### ENABLE | DISABLE

Tells [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] whether to gather full-text index data for *table_name*. ENABLE activates the full-text index; DISABLE turns off the full-text index. The table won't support full-text queries while the index is disabled.

Disabling a full-text index allows you to turn off change tracking but keep the full-text index, which you can reactivate at any time using ENABLE. When the full-text index is disabled, the full-text index metadata remains in the system tables. If CHANGE_TRACKING is in the enabled state (automatic or manual update) when the full-text index is disabled, the state of the index freezes, any ongoing crawl stops, and new changes to the table data aren't tracked or propagated to the index.

#### SET CHANGE_TRACKING { MANUAL | AUTO | OFF }

Specifies whether changes (updates, deletes, or inserts) made to table columns that are covered by the full-text index will be propagated by [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] to the full-text index. Data changes through WRITETEXT and UPDATETEXT aren't reflected in the full-text index, and aren't picked up with change tracking.

> [!NOTE]  
> For more information, see [Interactions of Change Tracking and NO POPULATION Parameter](#change-tracking-no-population).

- MANUAL

  Specifies that the tracked changes are propagated manually by calling the ALTER FULLTEXT INDEX ... START UPDATE POPULATION [!INCLUDE [tsql](../../includes/tsql-md.md)] statement (*manual population*). You can use [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] Agent to call this [!INCLUDE [tsql](../../includes/tsql-md.md)] statement periodically.

- AUTO

  Specifies that the tracked changes are propagated automatically as data is modified in the base table (*automatic population*). Although changes are propagated automatically, these changes might not be reflected immediately in the full-text index. AUTO is the default.

- OFF

  Specifies that [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] doesn't keep a list of changes to the indexed data.

#### ADD | DROP *column_name*

Specifies the columns to be added or deleted from a full-text index. The column or columns must be of type **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary**, or **varbinary(max)**.

Use the DROP clause only on columns that have been enabled previously for full-text indexing.

Use TYPE COLUMN and LANGUAGE with the ADD clause to set these properties on the *column_name*. When a column is added, the full-text index on the table must be repopulated in order for full-text queries against this column to work.

> [!NOTE]  
> Whether the full-text index is populated after a column is added or dropped from a full-text index depends on whether change-tracking is enabled and whether WITH NO POPULATION is specified. For more information, see [Interactions of Change Tracking and NO POPULATION Parameter](#change-tracking-no-population).

#### TYPE COLUMN *type_column_name*

Specifies the name of a table column, *type_column_name*, which is used to hold the document type for a **varbinary**, **varbinary(max)**, or **image** document. This column, known as the type column, contains a user-supplied file extension (`.doc`, `.pdf`, `.xls`, and so forth). The type column must be of type **char**, **nchar**, **varchar**, or **nvarchar**.

Specify TYPE COLUMN *type_column_name* only if *column_name* specifies a **varbinary**, **varbinary(max)** or **image** column, in which data is stored as binary data; otherwise, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] returns an error.

> [!NOTE]  
> At indexing time, the Full-Text Engine uses the abbreviation in the type column of each table row to identify which full-text search filter to use for the document in *column_name*. The filter loads the document as a binary stream, removes the formatting information, and sends the text from the document to the word-breaker component. For more information, see [Configure and Manage Filters for Search](../../relational-databases/search/configure-and-manage-filters-for-search.md).

#### LANGUAGE *language_term*

The language of the data stored in *column_name*.

*language_term* is optional and can be specified as a string, integer, or hexadecimal value corresponding to the locale identifier (LCID) of a language. If *language_term* is specified, the language it represents is applied to all elements of the search condition. If no value is specified, the default full-text language of the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] instance is used.

Use the `sp_configure` stored procedure to access information about the default full-text language of the [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] instance.

When specified as a string, *language_term* corresponds to the `alias` column value in the `sys.syslanguages` system table. The string must be enclosed in single quotation marks, as in '*language_term*'. When specified as an integer, *language_term* is the actual LCID that identifies the language. When specified as a hexadecimal value, *language_term* is 0x followed by the hex value of the LCID. The hex value must not exceed eight digits, including leading zeros.

If the value is in double-byte character set (DBCS) format, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] converts it to Unicode.

Resources, such as word breakers and stemmers, must be enabled for the language specified as *language_term*. If such resources don't support the specified language, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] returns an error.

For non-BLOB and non-XML columns containing text data in multiple languages, or for cases when the language of the text stored in the column is unknown, use the neutral (0x0) language resource. For documents stored in XML- or BLOB-type columns, the language encoding within the document is used at indexing time. For example, in XML columns, the `xml:lang` attribute in XML documents identifies the language. At query time, the value previously specified in *language_term* becomes the default language used for full-text queries unless *language_term* is specified as part of a full-text query.

#### STATISTICAL_SEMANTICS

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Creates the additional key phrase and document similarity indexes that are part of statistical semantic indexing. For more information, see [Semantic Search (SQL Server)](../../relational-databases/search/semantic-search-sql-server.md).

#### [ , *...n* ]

Indicates that multiple columns may be specified for the ADD, ALTER, or DROP clauses. When multiple columns are specified, separate these columns with commas.

#### WITH NO POPULATION

Specifies that the full-text index won't be populated after an ADD or DROP column operation or a SET STOPLIST operation. The index is only populated if the user executes a START...POPULATION command.

When NO POPULATION is specified, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] doesn't populate an index. The index is populated only after the user gives an ALTER FULLTEXT INDEX...START POPULATION command. When NO POPULATION isn't specified, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] populates the index.

If CHANGE_TRACKING is enabled and WITH NO POPULATION is specified, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] returns an error. If CHANGE_TRACKING is enabled and WITH NO POPULATION isn't specified, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] performs a full population on the index.

> [!NOTE]  
> For more information, see [Interactions of Change Tracking and NO POPULATION Parameter](#change-tracking-no-population).

#### {ADD | DROP } STATISTICAL_SEMANTICS

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Enables or disables statistical semantic indexing for the specified columns. For more information, see [Semantic Search (SQL Server)](../../relational-databases/search/semantic-search-sql-server.md).

#### START { FULL | INCREMENTAL | UPDATE } POPULATION

Tells [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] to begin population of the full-text index of *table_name*. If a full-text index population is already in progress, [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] returns a warning and doesn't start a new population.

- FULL

  Specifies that every row of the table is retrieved for full-text indexing even if the rows have already been indexed.

- INCREMENTAL

  Specifies that only the modified rows since the last population is retrieved for full-text indexing. INCREMENTAL can be applied only if the table has a column of the type **timestamp**. If a table in the full-text catalog doesn't contain a column of the type **timestamp**, the table undergoes a FULL population.

- UPDATE

  Specifies the processing of all insertions, updates, or deletions since the last time the change-tracking index was updated. Change-tracking population must be enabled on a table, but the background update index or the auto change tracking shouldn't be turned on.

#### {STOP | PAUSE | RESUME } POPULATION

Stops, or pauses any population in progress; or stops or resumes any paused population.

STOP POPULATION doesn't stop auto change tracking or background update index. To stop change tracking, use SET CHANGE_TRACKING OFF.

PAUSE POPULATION and RESUME POPULATION can only be used for full populations. They aren't relevant to other population types because the other populations resume crawls from where the crawl stopped.

#### SET STOPLIST { OFF | SYSTEM | *stoplist_name* }

Changes the full-text stoplist that is associated with the index, if any.

- OFF

  Specifies that no stoplist is associated with the full-text index.

- SYSTEM

  Specifies that the default full-text system STOPLIST should be used for this full-text index.

- *stoplist_name*

  Specifies the name of the stoplist to be associated with the full-text index.

For more information, see [Configure and Manage Stopwords and Stoplists for Full-Text Search](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

#### SET SEARCH PROPERTY LIST { OFF | *property_list_name* } [ WITH NO POPULATION ]

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

Changes the search property list that is associated with the index, if any.

- OFF

  Specifies that no property list is associated with the full-text index. When you turn off the search property list of a full-text index (`ALTER FULLTEXT INDEX ... SET SEARCH PROPERTY LIST OFF`), property searching on the base table is no longer possible.

  By default, when you turn off an existing search property list, the full-text index automatically repopulates. If you specify WITH NO POPULATION when you turn off the search property list, automatic repopulation doesn't occur. However, we recommend that you eventually run a full population on this full-text index at your convenience. Repopulating the full-text index removes the property-specific metadata of each dropped search property, making the full-text index smaller and more efficient.

- *property_list_name*

  Specifies the name of the search property list to be associated with the full-text index.

  Adding a search property list to a full-text index requires repopulating the index to index the search properties that are registered for the associated search property list. If you specify WITH NO POPULATION when adding the search property list, you need to run a population on the index, at an appropriate time.

> [!IMPORTANT]  
> If the full-text index was previously associated with a different search it must be rebuilt property list in order to bring the index into a consistent state. The index is truncated immediately and is empty until the full population runs. For more information, see [Changing the Search Property List Causes Rebuilding the Index](#change-search-property-rebuild-index).

> [!NOTE]  
> You can associate a given search property list with more than one full-text index in the same database.

**Find the search property lists on the current database**

- [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)

For more information about search property lists, see [Search Document Properties with Search Property Lists](../../relational-databases/search/search-document-properties-with-search-property-lists.md).

## Remarks

On **xml** columns, you can create a full-text index that indexes the content of the XML elements, but ignores the XML markup. Attribute values are full-text indexed unless they are numeric values. Element tags are used as token boundaries. Well-formed XML or HTML documents and fragments containing multiple languages are supported. For more information, see [Use Full-Text Search with XML Columns](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).

We recommend that the index key column is an integer data type. This provides optimizations at query execution time.

ALTER FULLTEXT INDEX can't be placed inside a user transaction. This statement must be run in its own implicit transaction.

For more information about full-text indexes, see [Create and Manage Full-Text Indexes](../../relational-databases/search/create-and-manage-full-text-indexes.md).

## <a id="change-tracking-no-population"></a> Interactions of change tracking and NO POPULATION parameter

Whether the full-text index is populated depends on whether change-tracking is enabled and whether WITH NO POPULATION is specified in the ALTER FULLTEXT INDEX statement. The following table summarizes the result of their interaction.

| Change tracking | WITH NO POPULATION | Result |
| --- | --- | --- |
| Not enabled | Not specified | A full population is performed on the index. |
| Not enabled | Specified | No population of the index occurs until an ALTER FULLTEXT INDEX...START POPULATION statement is issued. |
| Enabled | Specified | An error is raised, and the index isn't altered. |
| Enabled | Not specified | A full population is performed on the index. |

For more information about populating full-text indexes, see [Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md).

## <a id="change-search-property-rebuild-index"></a> Change the search property list causes rebuilding the index

The first time that a full-text index is associated with a search property list, the index must be repopulated to index property-specific search terms. The existing index data isn't truncated.

However, if you associate the full-text index with a different property list, the index is rebuilt. Rebuilding immediately truncates the full-text index, removing all existing data, and the index must be repopulated. While the population progresses, full-text queries on the base table search only on the table rows that have already been indexed by the population. The repopulated index data includes metadata from the registered properties of the newly added search property list.

Scenarios that cause rebuilding include:

- Switch directly to a different search property list (see "Scenario A," later in this section).

- Turn off the search property list, and later associate the index with any search property list (see "Scenario B," later in this section).

> [!NOTE]  
> For more information about how full-text search works with search property lists, see [Search Document Properties with Search Property Lists](../../relational-databases/search/search-document-properties-with-search-property-lists.md). For information about full populations, see [Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md).

### Scenario A: Switch directly to a different search property list

1. A full-text index is created on `table_1` with a search property list `spl_1`:

   ```sql
   CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index
       WITH SEARCH PROPERTY LIST=spl_1,
       CHANGE_TRACKING OFF, NO POPULATION;
   ```

1. A full population is run on the full-text index:

   ```sql
   ALTER FULLTEXT INDEX ON table_1 START FULL POPULATION;
   ```

1. The full-text index is later associated a different search property list, `spl_2`, using the following statement:

   ```sql
   ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_2;
   ```

   This statement causes a full population, the default behavior.  However, before beginning this population, the Full-Text Engine automatically truncates the index.

### Scenario B: Turn off the search property list and later associate the index with any search property list

1. A full-text index is created on `table_1` with a search property list `spl_1`, followed by an automatic full population (the default behavior):

   ```sql
   CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index
       WITH SEARCH PROPERTY LIST=spl_1;
   ```

1. The search property list is turned off, as follows:

   ```sql
   ALTER FULLTEXT INDEX ON table_1
       SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;
   ```

1. The full-text index is once more associated either the same search property list or a different one.

   For example, the following statement reassociates the full-text index with the original search property list, `spl_1`:

   ```sql
   ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_1;
   ```

   This statement starts a full population, the default behavior.

   > [!NOTE]  
   > The rebuild would also be required for a different search property list, such as `spl_2`.

## Permissions

The user must have ALTER permission on the table or indexed view, or be a member of the **sysadmin** fixed server role, or the **db_ddladmin** or **db_owner** fixed database roles.

If SET STOPLIST is specified, the user must have REFERENCES permission on the stoplist. If SET SEARCH PROPERTY LIST is specified, the user must have REFERENCES permission on the search property list. The owner of the specified stoplist or search property list can grant REFERENCES permission, if the owner has  ALTER FULLTEXT CATALOG permissions.

> [!NOTE]  
> The public is granted REFERENCES permission to the default stoplist that is shipped with [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].

## Examples

### A. Set manual change tracking

The following example sets manual change tracking on the full-text index on the `JobCandidate` table.

```sql
USE AdventureWorks2022;
GO
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate
   SET CHANGE_TRACKING MANUAL;
GO
```

### B. Associate a property list with a full-text index

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

The following example associates the `DocumentPropertyList` property list with the full-text index on the `Production.Document` table. This ALTER FULLTEXT INDEX statement starts a full population, which is the default behavior of the SET SEARCH PROPERTY LIST clause.

> [!NOTE]  
> For an example that creates the `DocumentPropertyList` property list, see [CREATE SEARCH PROPERTY LIST (Transact-SQL)](create-search-property-list-transact-sql.md).

```sql
USE AdventureWorks2022;
GO
ALTER FULLTEXT INDEX ON Production.Document
   SET SEARCH PROPERTY LIST DocumentPropertyList;
GO
```

### C. Remove a search property list

**Applies to**: [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] and later versions.

The following example removes the `DocumentPropertyList` property list from the full-text index on the `Production.Document`. In this example, there's no hurry for removing the properties from the index, so the WITH NO POPULATION option is specified. However, property-level searching is longer allowed against this full-text index.

```sql
USE AdventureWorks2022;
GO
ALTER FULLTEXT INDEX ON Production.Document
   SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;
GO
```

### D. Start a full population

The following example starts a full population on the full-text index on the `JobCandidate` table.

```sql
USE AdventureWorks2022;
GO
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate
   START FULL POPULATION;
GO
```

## See also

- [sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)
- [CREATE FULLTEXT INDEX (Transact-SQL)](create-fulltext-index-transact-sql.md)
- [DROP FULLTEXT INDEX (Transact-SQL)](drop-fulltext-index-transact-sql.md)
- [Full-Text Search](../../relational-databases/search/full-text-search.md)
- [Populate Full-Text Indexes](../../relational-databases/search/populate-full-text-indexes.md)
