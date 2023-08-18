---
title: Save (Not Permitted) Dialog Box
description: "Save (Not Permitted) Dialog Box"
author: markingmyname
ms.author: maghan
ms.date: 01/19/2017
ms.service: sql
ms.subservice: ssms
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.table.tablerecreatenosave.f1"
---
# Save (Not Permitted) Dialog Box
[!INCLUDE[SQL Server](../../includes/applies-to-version/sqlserver.md)]
The **Save** (Not Permitted) dialog box warns you that saving changes is not permitted because the changes you have made require the listed tables to be dropped and re-created.  
  
The following actions might require a table to be re-created:  
  
-   Adding a new column to the middle of the table  
  
-   Dropping a column  
  
-   Changing column nullability  
  
-   Changing the order of the columns  
  
-   Changing the data type of a column  
  
To change this option, on the **Tools** menu, click **Options**, expand **Designers**, and then click **Table and Database Designers**. Select or clear the **Prevent saving changes that require the table to be re-created** check box.  
  
