---
title: Add Table Dialog Box (Query and View Designers)
description: "Add Table Dialog Box (Query and View Designers) (Visual Database Tools)"
author: markingmyname
ms.author: maghan
ms.date: 01/19/2017
ms.service: sql
ms.subservice: ssms
ms.topic: conceptual
f1_keywords:
  - "vdt.dlgbox.query.addtable"
  - "vdtsql.chm:65565"
---

# Add Table Dialog Box (Query and View Designers) (Visual Database Tools)

[!INCLUDE[SQL Server](../../includes/applies-to-version/sqlserver.md)]
This dialog box lets you add tables, views, user-defined functions, or synonyms to a query or view.  
  
> [!NOTE]  
> If the table is published for replication, you must make schema changes using the Transact-SQL statement [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) or SQL Server Management Objects (SMO). When schema changes are made using the Table Designer or the Database Diagram Designer, it attempts to drop and recreate the table. You cannot drop published objects, therefore the schema change will fail.  
  
## Options  
**Tables**  
Lists the tables you can add to the **Diagram** pane. To add a table, select it and click **Add**. To add several tables at once, select them and click **Add**.  
  
**Views**  
Lists the views you can add to the **Diagram** pane. To add a view, select it and click **Add**. To add several views at once, select them and click **Add**.  
  
**Functions**  
Lists the user-defined functions you can add to the **Diagram** pane. To add a function, select it and click **Add**. To add several functions at once, select them and click **Add**.  
  
**Synonyms**  
Lists the synonyms you can add to the **Diagram** pane. To add a synonym, select it and click **Add**. To add several synonyms at once, select them and click **Add**.  
  
**Refresh**  
Update the list to include any changes made to the database since the list was last retrieved.  
  
**Add**  
Add the selected item or items.  
  
## See Also  
[Design Queries and Views How-to Topics &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
