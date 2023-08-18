---
title: "PDOStatement::setAttribute"
description: "API reference for the PDOStatement::setAttribute function in the Microsoft PDO_SQLSRV Driver for PHP for SQL Server."
author: David-Engel
ms.author: v-davidengel
ms.date: "08/10/2020"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Sets an attribute value, either a predefined PDO attribute or a custom driver attribute.  
  
## Syntax  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### Parameters  
$*attribute*: An integer, one of the PDO::ATTR_* or PDO::SQLSRV_ATTR_\* constants. See the Remarks section for the list of available attributes.  
  
$*value*: The (mixed) value to be set for the specified $*attribute*.  
  
## Return Value  
TRUE on success, FALSE otherwise.  
  
## Remarks  
The following table contains the list of available attributes:  
  
|Attribute|Values|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 to the PHP memory limit.|Configures the size of the buffer that holds the result set for a client-side cursor.<br /><br />The default is 10,240 KB (10 MB).<br /><br />For more information about client-side cursors, see [Cursor Types &#40;PDO_SQLSRV Driver&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DATA_CLASSIFICATION|true or false|Specifies whether to retrieve data classification metadata when calling [PDOStatement::getColumnMeta](../../connect/php/pdostatement-getcolumnmeta.md). The default is false.|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|Integer between 0 and 4 (inclusive)|Specifies the number of decimal places when formatting fetched money values.<br /><br />Any negative integer or value more than 4 will be ignored.<br /><br />This option works only when PDO::SQLSRV_ATTR_FORMAT_DECIMALS is true.<br /><br />This option may also be set at the connection level. If so, then this option overrides the connection level option.<br /><br />For more information, see [Formatting Decimal Strings and Money Values (PDO_SQLSRV Driver)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (Default)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Sets the character set encoding to be used by the driver to communicate with the server.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true or false|Specifies whether to retrieve date and time types as [PHP DateTime](http://php.net/manual/en/class.datetime.php) objects. If left false, the default behavior is to return them as strings.<br /><br />This option may also be set at the connection level. If so, then this option overrides the connection level option.<br /><br />For more information, see [How to: Retrieve Date and Time Types as PHP DateTime Objects Using the PDO_SQLSRV Driver](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true or false|Handles numeric fetches from columns with numeric SQL types (bit, integer, smallint, tinyint, float, or real).<br /><br />When connection option flag ATTR_STRINGIFY_FETCHES is on, the return value is a string even when SQLSRV_ATTR_FETCHES_NUMERIC_TYPE is on.<br /><br />When the returned PDO type in bind column is PDO_PARAM_INT, the return value from an integer column is an int even if SQLSRV_ATTR_FETCHES_NUMERIC_TYPE is off.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true or false|Specifies whether to add leading zeroes to decimal strings when appropriate. If set, this option enables the PDO::SQLSRV_ATTR_DECIMAL_PLACES option for formatting money types. If left false, the default behavior of returning exact precision and omitting leading zeroes for values less than 1 is used.<br /><br />This option may also be set at the connection level. If so, then this option overrides the connection level option.<br /><br />For more information, see [Formatting Decimal Strings and Money Values (PDO_SQLSRV Driver)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|Sets the query timeout in seconds.<br /><br />By default, the driver will wait indefinitely for results. Negative numbers are not allowed.<br /><br />0 means no timeout.|  
  
## Example  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## See Also  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
