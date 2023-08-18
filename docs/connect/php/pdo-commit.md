---
title: "PDO::commit"
description: "API reference for the PDO::commit function in the Microsoft PDO_SQLSRV Driver for PHP for SQL Server."
author: David-Engel
ms.author: v-davidengel
ms.date: "08/10/2020"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Sends commands to the database that were issued after calling [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) and returns the connection to auto commit mode.  
  
## Syntax  
  
```  
  
bool PDO::commit();  
```  
  
## Return Value  
true if the method call succeeded, false otherwise.  
  
## Remarks  
PDO::commit is not affected by (and does not affect) the value of PDO::ATTR_AUTOCOMMIT.  
  
See [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) for an example that uses PDO::commit.  
  
Support for PDO was added in version 2.0 of the [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## See Also  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
