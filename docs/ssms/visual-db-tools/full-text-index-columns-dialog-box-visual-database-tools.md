---
title: Full-Text Index Columns Dialog Box
description: "Full-Text Index Columns Dialog Box (Visual Database Tools)"
author: markingmyname
ms.author: maghan
ms.date: 01/19/2017
ms.service: sql
ms.subservice: ssms
ms.topic: conceptual
f1_keywords:
  - "vdt.dlgbox.fulltextcolumn"
---
# Full-Text Index Columns Dialog Box (Visual Database Tools)
[!INCLUDE[SQL Server](../../includes/applies-to-version/sqlserver.md)]
This dialog box lists the columns participating in the full-text index for the table open in Table Designer. To access this dialog box, right-click the table in Table Designer, choose **Full-Text Index**, and in the **Full-Text Index** dialog box, click the index with columns you want to view or edit, click the **Columns** field in the grid to the right, and click the ellipses (**...**).  
  
## Options  
**Column**  
Shows the names of columns participating in the full-text index. To add a column, click in the first empty cell and choose a column from the drop-down list. Only columns with either text-based or image data types will be accessible.  
  
**Data Type**  
Shows the data type for each column. This is a read-only property. To change a data type, open the table in Table Designer, click the column, and edit the data type in the **Column Properties** tab.  
  
**Typed by Column**  
Applies only to columns with the data type **image**. Provides a drop-down list from which you can choose which of the other columns represent the data type of this column. If this column is not of the **image** data type the value will be None.  
  
Columns with the data type **image** can contain Microsoft Office files (.doc, .xls, and .ppt files), text files (.txt files), and HTML files (.htm files), and setting the data type of that column to image allows the full-text search to search the contents of the files.  
  
**Language**  
Lists available languages. Choose the language from the drop-down list appropriate for your column data. For example, if you are using an English operating system, but you want to index a column that contains German text, choose German from the drop-down list to improve the index's performance.  
  
**Statistical Semantics**  
Select whether to enable semantic indexing for the selected column. For more information, see [Semantic Search placeholder](../../relational-databases/search/semantic-search-sql-server.md).  
  
If you select a **Language** prior to selecting **Statistical Semantics**, and the selected language does not have an associated Semantic Language Model, then the **Statistical Semantics** checkbox is disabled. If you select **Statistical Semantics** prior to selecting a **Language**, the languages available in the drop-down combo box will be restricted to those for which there is Semantic Language Model support.  
  
## See Also  
[Full-Text Index Dialog Box &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/full-text-index-dialog-box-visual-database-tools.md)  
