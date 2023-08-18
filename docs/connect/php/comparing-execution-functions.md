---
title: "Comparing execution functions"
description: "This topic lists the different query execution functions when using the Microsoft Drivers for PHP for SQL Server"
author: David-Engel
ms.author: v-davidengel
ms.date: "08/10/2020"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "executing queries"
---
# Comparing Execution Functions
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

The [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] provides several options for executing functions.  

## SQLSRV Execution Functions  
If you are using the SQLSRV driver, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) to execute a single query and [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) with [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) to execute a prepared statement multiple times with different parameter values for each execution.  

## PDO_SQLSRV Execution Functions 
If you are using the PDO_SQLSRV driver, you can execute a query with one of the following:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) and [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## See Also  
[SQLSRV Driver API Reference](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV Driver Reference](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Programming Guide for the Microsoft Drivers for PHP for SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
