---
title: Navigate Between Scripts
description: Find out how to navigate between scripts in the Transact-SQL Editor. View examples that show how to use tools such as Go To Definition and Find All References.
author: markingmyname
ms.author: maghan
ms.date: 02/09/2017
ms.service: sql
ms.subservice: ssdt
ms.topic: conceptual
f1_keywords:
  - "sql.data.tools.editor.howto.navigate"
---

# How to: Navigate Between Scripts

The Transact\-SQL Editor for offline development provides two useful navigation tools that are familiar to Visual Studio users: Go To Definition and Find All References. For example, you can right-click a table name and use "Find All References" to list all references to the table in the project. You can double-click a search result to go to the specific code file. In this file, you can right-click the table name again, and choose "Go to Definition" to go back to the table definition.  
  
> [!WARNING]  
> The following procedure uses entities created in previous procedures in the [Connected Database Development](../ssdt/connected-database-development.md) and [Project-Oriented Offline Database Development](../ssdt/project-oriented-offline-database-development.md) sections.  
  
### To navigate between scripts  
  
1.  Expand the **Functions** folder in **Solution Explorer** and double-click **GetProductsBySupplier.sql**.  
  
2.  Right-click `Products` in this line of code and select **Go To Definition**  
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql is automatically opened, showing the location where the `Products` type is defined.  
  
4.  Go back to GetProductsBySupplier.sql. This time select **Find All References** in the contextual menu for `Products`. In the **Find Symbol Results** pane, you will see a list of locations where the `Products` table is referenced. Double-clicking any of the search results will bring you to the location of the reference.  
  
