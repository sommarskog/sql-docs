---
title: "Procedures"
description: "Procedures"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: native-client
ms.topic: "reference"
helpviewer_keywords:
  - "stored procedures [ODBC]"
  - "stored procedures [ODBC], about ODBC stored procedures"
  - "ODBC applications, statements"
  - "statements [ODBC], stored procedures"
  - "ODBC applications, stored procedures"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Procedures
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A stored procedure is a precompiled executable object that contains one or more [!INCLUDE[tsql](../../../includes/tsql-md.md)] statements. Stored procedures can have input and output parameters and can also put out an integer return code. An application can enumerate available stored procedures by using catalog functions.  
  
 ODBC applications that target [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] should only use direct execution to call a stored procedure. When connected to earlier versions of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC driver implements [SQLPrepare Function](../../../odbc/reference/syntax/sqlprepare-function.md) by creating a temporary stored procedure, which is then called on **SQLExecute**. It adds overhead to have **SQLPrepare** create a temporary stored procedure that only calls the target stored procedure versus directly executing the target stored procedure. Even when connected to an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], preparing a call requires an extra round trip across the network and the building of an execution plan that just calls the stored procedure execution plan.  
  
 ODBC applications should use the ODBC CALL syntax when executing a stored procedure. The driver is optimized to use a remote procedure call mechanism to call the procedure when the ODBC CALL syntax is used. This is more efficient than the mechanism used to send a [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE statement to the server.  
  
 For more information, see [Running Stored Procedures](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## See Also  
 [Executing Statements &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
