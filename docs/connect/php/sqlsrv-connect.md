---
title: "sqlsrv_connect"
description: "Creates a connection resource and opens a connection using the sql_srv driver for PHP. By default, the connection is attempted using Windows Authentication."
author: David-Engel
ms.author: v-davidengel
ms.date: "03/26/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "connecting to the server"
  - "API Reference, sqlsrv_connect"
  - "connection pooling support"
  - "sqlsrv_connect"
apiname: "sqlsrv_connect"
apitype: "NA"
---
# sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Creates a connection resource and opens a connection. By default, the connection is attempted using Windows Authentication.  
  
## Syntax  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### Parameters  
*$serverName*: A string specifying the name of the server to which a connection is being established. An instance name (for example, "myServer\instanceName") or port number (for example, "myServer, 1521") can be included as part of this string. For a complete description of the options available for this parameter, see the Server keyword in the ODBC Driver Connection String Keywords section of [Using Connection String Keywords with SQL Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
Beginning in version 3.0 of the [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], you can also specify a LocalDB instance with `"(localdb)\instancename"`. For more information, see [Support for LocalDB](php-driver-for-sql-server-support-for-localdb.md).  
  
Also beginning in version 3.0 of the [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], you can specify a virtual network name, to connect to an Always On availability group. For more information about [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] support for [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], see [Support for High Availability, Disaster Recovery](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [OPTIONAL]: An associative **array** that contains connection attributes (for example, **array**("Database" => "AdventureWorks")). See [Connection Options](connection-options.md) for a list of the supported keys for the array.  
  
## Return Value  
A PHP connection resource. If a connection cannot be successfully created and opened, **false** is returned.  
  
## Remarks  
If values for the *UID* and *PWD* keys are not specified in the optional *$connectionInfo* parameter, the connection will be attempted using Windows Authentication. For more information about connecting to the server, see [How to: Connect Using Windows Authentication](how-to-connect-using-windows-authentication.md) and [How to: Connect Using SQL Server Authentication](how-to-connect-using-sql-server-authentication.md).  
  
## Example  
The following example creates and opens a connection using Windows Authentication. The example assumes that SQL Server and the AdventureWorks database are installed on the local computer. All output is written to the console when the example is run from the command line.  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## See Also  
[SQLSRV Driver API Reference](sqlsrv-driver-api-reference.md)

[Connecting to the Server](connecting-to-the-server.md)

[About Code Examples in the Documentation](about-code-examples-in-the-documentation.md)  
  
