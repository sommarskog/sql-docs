---
title: "Hints (Transact-SQL)"
description: "Hints (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "08/09/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
helpviewer_keywords:
  - "query optimizer [SQL Server], hints"
  - "hints [SQL Server], about hints"
  - "SELECT statement [SQL Server], hints"
  - "hints [SQL Server]"
  - "INSERT statement [SQL Server], hints"
  - "UPDATE statement [SQL Server], hints"
  - "DELETE statement [SQL Server], hints"
dev_langs:
  - "TSQL"
---
# Hints (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Hints are options or strategies specified for enforcement by the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] query processor on SELECT, INSERT, UPDATE, or DELETE statements. The hints override any execution plan the query optimizer might select for a query.  
  
> [!CAUTION]  
>  Because the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] query optimizer typically selects the best execution plan for a query, we recommend that \<join_hint>, \<query_hint>, and \<table_hint> be used only as a last resort by experienced developers and database administrators.
  
 The following hints are described in this section:  
  
-   [Join Hints](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Query Hints](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Table Hint](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
