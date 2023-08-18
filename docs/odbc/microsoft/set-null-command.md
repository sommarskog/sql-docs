---
title: "SET NULL Command"
description: "SET NULL Command"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "set nullSET NULL"
---
# SET NULL Command
Determines how null values are supported by the ALTER TABLE - SQL, CREATE TABLE - SQL, and INSERT - SQL commands.  
  
## Syntax  
  
```  
  
SET NULL ON | OFF  
```  
  
## Arguments  
 ON  
 (Default for the driver; the default for Visual FoxPro is OFF.) Specifies that all columns in a table created with ALTER TABLE and CREATE TABLE will allow null values. You can override null value support for columns in the table by including the NOT NULL clause in the columns' definitions.  
  
 Also specifies that INSERT - SQL will insert null values into any columns not included in the INSERT - SQL VALUE clause. INSERT - SQL will insert null values only into columns that allow null values.  
  
 OFF  
 Specifies that all columns in a table created with ALTER TABLE and CREATE TABLE will not allow null values. You can designate null value support for columns in ALTER TABLE and CREATE TABLE by including the NULL clause in the columns' definitions.  
  
 Also specifies that INSERT - SQL will insert blank values into any columns not included in the INSERT - SQL VALUE clause.  
  
## Remarks  
 SET NULL affects only how null values are supported by ALTER TABLE, CREATE TABLE, and INSERT - SQL. Other commands are unaffected by SET NULL.  
  
## See Also  
 [ALTER TABLE - SQL Command](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE - SQL Command](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL Command](../../odbc/microsoft/insert-sql-command.md)
