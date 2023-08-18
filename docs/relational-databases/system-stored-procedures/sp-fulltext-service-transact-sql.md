---
title: "sp_fulltext_service (Transact-SQL)"
description: Changes the server properties of full-text search for SQL Server.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 07/07/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_fulltext_service"
  - "sp_fulltext_service_TSQL"
helpviewer_keywords:
  - "full-text search [SQL Server], properties"
  - "sp_fulltext_service"
  - "Full-Text Search Upgrade Option"
dev_langs:
  - "TSQL"
---
# sp_fulltext_service (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Changes the server properties of full-text search for [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_fulltext_service
    [ [ @action = ] N'action' ]
    [ , [ @value = ] value ]
[ ; ]
```

## Arguments

#### [ @action = ] N'*action*'

The property to be changed or reset. *@action* is **nvarchar(100)**, with no default. For a list of *@action* properties, their descriptions, and the values that can be set, see the table under the *@value* argument.

This argument returns the following properties:

- data type
- current running value
- minimum or maximum value
- deprecation status, if applicable.

#### [ @value = ] *value*

*@value* is **sql_variant**, with a default of `NULL`.

The value of the specified property. *@value* is **sql_variant**, with a default value of NULL. If *@value* is null, `sp_fulltext_service` returns the current setting. This table lists action properties, their descriptions, and the values that can be set.

> [!NOTE]  
> The following actions will be removed in a future release of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]: **clean_up**, **connect_timeout**, **data_timeout**, and **resource_usage**. Avoid using these actions in new development work, and plan to modify applications that currently use any of them.

| Action | Data type | Description |
| --- | --- | --- |
| **clean_up** | **int** | Supported for backward compatibility only. The value is always `0`. |
| **connect_timeout** | **int** | Supported for backward compatibility only. The value is always `0`. |
| **data_timeout** | **int** | Supported for backward compatibility only. The value is always `0`. |
| **load_os_resources** | **int** | Indicates whether operating system word breakers, stemmers, and filters are registered and used with this instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]. One of:<br /><br />0 = Use only filters and word breakers specific to this instance of [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />1 = Load operating system filters and word breakers.<br /><br />By default, this property is disabled to prevent inadvertent behavior changes by updates made to the operating system. Enabling use of operating system resources provides access to resources for languages and document types registered with [!INCLUDE [msCoName](../../includes/msconame-md.md)] Indexing Service that don't have an instance-specific resource installed. If you enable the loading of operating system resources, ensure that the operating system resources are trusted signed binaries; otherwise, they can't be loaded when **verify_signature** is set to 1. |
| **master_merge_dop** | **int** | Specifies the number of threads to be used by the master merge process. This value shouldn't exceed the number of available CPUs or CPU cores.<br /><br />When this argument isn't specified, the service uses the lesser of 4, or the number of available CPUs or CPU cores. |
| **pause_indexing** | **int** | Specifies whether full-text indexing should be paused, if it is currently running, or resumed, if it is currently paused.<br /><br />0 = Resumes full-text indexing activities for the server instance.<br /><br />1 = Pauses full-text indexing activities for the server instance. |
| **resource_usage** | **int** | Has no function in [!INCLUDE [sql2008-md](../../includes/sql2008-md.md)] and later versions, and is ignored. |
| **update_languages** | NULL | Updates the list of languages and filters that are registered with full-text search. The languages are specified when configuring indexing and in full-text queries. Filters are used by the filter daemon host to extract textual information from corresponding file formats such as .docx stored in data types, such as **varbinary**, **varbinary(max)**, **image**, or **xml**, for full-text indexing.<br /><br />For more information, see [View or Change Registered Filters and Word Breakers](../search/view-or-change-registered-filters-and-word-breakers.md). |
| **upgrade_option** | **int** | Controls how full-text indexes are migrated when upgrading a database from [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] to a later version. This property applies to upgrading by attaching a database, restoring a database backup, restoring a file backup, or copying the database by using the Copy Database Wizard.<br /><br />One of:<br /><br />0 = Full-text catalogs are rebuilt using the new and enhanced word breakers. Rebuilding indexes can take some time, and a significant amount of CPU and memory might be required after the upgrade.<br /><br />1 = Full-text catalogs are reset. [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] full-text catalog files are removed, but the metadata for full-text catalogs and full-text indexes is retained. After being upgraded, all full-text indexes are disabled for change tracking and crawls aren't started automatically. The catalog will remain empty until you manually issue a full population, after the upgrade completes.<br /><br />2 = Full-text catalogs are imported. Typically, import is faster than rebuild. For example, when using only one CPU, import runs about 10 times faster than rebuild. However, an imported full-text catalog doesn't use the new and enhanced word breakers, so you might want to rebuild your full-text catalogs eventually.<br /><br />Note: Rebuild can run in multi-threaded mode, and if more than 10 CPUs are available, rebuild might run faster than import if you allow rebuild to use all of the CPUs.<br /><br />If a full-text catalog isn't available, the associated full-text indexes are rebuilt. This option is available for only [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] databases.<br /><br />For information about choosing a full-text upgrade option, see full-[Upgrade Full-Text Search](../search/upgrade-full-text-search.md).<br /><br />Note: To set this property in [!INCLUDE [ssManStudioFull](../../includes/ssmanstudiofull-md.md)], use the **Full-Text Upgrade Option** property. For more information, see [Manage and Monitor Full-Text Search for a Server Instance](../search/manage-and-monitor-full-text-search-for-a-server-instance.md). |
| **verify_signature** | **int** | Indicates whether the Full-Text Engine loads only signed binaries. By default, only trusted, signed binaries are loaded.<br /><br />1 = Verify that only trusted, signed binaries are loaded (default).<br /><br />0 = Don't verify whether binaries are signed. |

## Return code values

`0` (success) or `1` (failure).

## Result sets

None.

## Permissions

Only members of the **serveradmin** fixed server role or the system administrator can execute `sp_fulltext_service`.

## Examples

### A. Update the list of registered languages

The following example updates the list of languages registered with full-text search.

```sql
EXEC sp_fulltext_service 'update_languages';
GO
```

### B. Change the full-text upgrade option to reset full-text catalogs

The following example changes the full-text upgrade option to reset full-text catalogs, removing them completely. This example specifies the optional *@action* and *@value* arguments.

```sql
EXEC sp_fulltext_service
    @action = 'upgrade_option',
    @value = 1;
GO
```

## See also

- [Full-Text Search](../search/full-text-search.md)
- [FULLTEXTSERVICEPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)
- [System stored procedures (Transact-SQL)](system-stored-procedures-transact-sql.md)
