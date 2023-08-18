---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
description: DBCC PDW_SHOWEXECUTIONPLAN displays the execution plan for a query running on a specific Azure Synapse Analytics or Analytics Platform System (PDW) compute node or control node.
author: rwestMSFT
ms.author: randolphwest
ms.date: 12/05/2022
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "language-reference"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azure-sqldw-latest"
---

# DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Displays the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execution plan for a query running on a specific [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Compute node or Control node. Use this to troubleshoot query performance problems while queries are running on the Compute nodes and Control node.

Once query performance problems are understood for SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] queries running on the Compute nodes, there are several ways to improve performance. Possible ways to improve query performance on the Compute nodes include creating multi-column statistics, creating nonclustered indexes, or using query hints.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

Syntax for Azure Synapse Analytics:

```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id , spid )
[;]
```

Syntax for Analytics Platform System (PDW):

```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id , spid )
[;]
```

> [!NOTE]  
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## Arguments

#### *distribution_id*

 Identifier for the distribution that is running the query plan. This is an integer and can't be `NULL`. Value must be between 1 and 60. Used when targeting [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].

#### *pdw_node_id*

 Identifier for the node that is running the query plan. This is an integer and can't be `NULL`. Used when targeting an Appliance.

#### *spid*

 Identifier for the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] session that is running the query plan. This is an integer and can't be `NULL`.

## Permissions

 Requires CONTROL permission on [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)].

Requires **VIEW SERVER STATE** permission on the Appliance.

## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)]

### A. DBCC PDW_SHOWEXECUTIONPLAN basic syntax

The following sample query will return the `sql_spid` for each actively running distribution.

```sql
SELECT [sql_spid]
    , [pdw_node_id]
    , [request_id]
    , [dms_step_index]
    , [type]
    , [start_time]
    , [end_time]
    , [status]
    , [distribution_id]
FROM sys.dm_pdw_dms_workers
WHERE [status] <> 'StepComplete'
    AND [status] <> 'StepError'
ORDER BY request_id
    , [dms_step_index];
```

If you are curious as to what `distribution_id` 1 was running in session 375, you would run the following command:

```sql
DBCC PDW_SHOWEXECUTIONPLAN (1, 375);
```

## Examples: Analytics Platform System (PDW)

### B. DBCC PDW_SHOWEXECUTIONPLAN basic syntax

 The query that is running too long is either running a DMS query plan operation or a SQL query plan operation.

If the query is running a DMS query plan operation, you can use the following query to retrieve a list of the node IDs and session IDs for steps that aren't complete.

```sql
SELECT [sql_spid]
    , [pdw_node_id]
    , [request_id]
    , [dms_step_index]
    , [type]
    , [start_time]
    , [end_time]
    , [status]
FROM sys.dm_pdw_dms_workers
WHERE [status] <> 'StepComplete'
    AND [status] <> 'StepError'
    AND pdw_node_id = 201001
ORDER BY request_id
    , [dms_step_index]
    , [distribution_id];
```

Based on the results of the preceding query, use the `sql_spid` and `pdw_node_id` as parameters to `DBCC PDW_SHOWEXECUTIONPLAN`. For example, the following command shows the execution plan for `pdw_node_id` 201001 and `sql_spid` 375.

```sql
DBCC PDW_SHOWEXECUTIONPLAN (201001, 375);
```

## Next steps

- [DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)](dbcc-pdw-showpartitionstats-transact-sql.md)
- [DBCC PDW_SHOWSPACEUSED (Transact-SQL)](dbcc-pdw-showspaceused-transact-sql.md)
- [Table size queries](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-overview#table-size-queries)
