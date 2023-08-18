---
title: "Ordinary Arguments"
description: "Ordinary Arguments"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "arguments in catalog functions [ODBC], ordinary"
  - "catalog functions [ODBC], arguments"
  - "ordinary arguments [ODBC]"
---
# Ordinary Arguments
When a catalog function string argument is an ordinary argument, it is treated as a literal string. An ordinary argument accepts neither a string search pattern nor a list of values. The case of an ordinary argument is significant, and quote characters in the string are taken literally. These arguments are treated as ordinary arguments if the SQL_ATTR_METADATA_ID statement attribute is set to SQL_FALSE; they are treated as identifier arguments instead if this attribute is set to SQL_TRUE.  
  
 If an ordinary argument is set to a null pointer and the argument is a required argument, the function returns SQL_ERROR and SQLSTATE HY009 (Invalid use of null pointer). If an ordinary argument is set to a null pointer and the argument is not a required argument, the argument's behavior is driver-dependent. The required arguments are listed in the following table.  
  
|Function|Required arguments|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
