---
title: "Using Server Cursors"
description: "Using Server Cursors"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: native-client
ms.topic: "reference"
helpviewer_keywords:
  - "ODBC applications, cursors"
  - "cursors [ODBC], server cursors"
  - "ODBC cursors, server cursors"
  - "server cursors [SQL Server]"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Using Server Cursors
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  If an ODBC application sets any of the ODBC cursor attributes to anything other than the defaults, the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC driver requests the server to implement an API server cursor of the same type. Using API server cursors frees memory on the client and can significantly reduce network traffic between the client and server.  
  
 A potential drawback of API server cursors is that they currently do not support all SQL statements. API server cursors cannot be used to execute:  
  
-   Batches or stored procedures that return multiple result sets.  
  
-   SELECT statements that contain COMPUTE, COMPUTE BY, FOR BROWSE, or INTO clauses.  
  
-   An EXECUTE statement referencing a remote stored procedure.  
  
 When connected to an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], executing a statement with these characteristics using a server cursor causes the cursor being converted to a default result set. When connected to earlier versions of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], it causes an error.  
  
## See Also  
 [How Cursors Are Implemented](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
