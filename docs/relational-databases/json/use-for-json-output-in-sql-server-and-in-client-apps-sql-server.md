---
title: "Use FOR JSON output in SQL Server and in client apps"
description: "Use FOR JSON output in SQL Server and in client apps (SQL Server)"
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.date: 06/03/2020
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "FOR JSON, using in client apps"
  - "FOR JSON, using in SQL Server"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Use FOR JSON output in SQL Server and in client apps (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

The following examples demonstrate some of the ways to use the **FOR JSON** clause and its JSON output in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or in client apps.  
  
## Use FOR JSON output in SQL Server variables  
The output of the FOR JSON clause is of type NVARCHAR(MAX), so you can assign it to any variable, as shown in the following example.  
  
```sql  
DECLARE @x NVARCHAR(MAX) =
  (SELECT TOP 10 *
     FROM Sales.SalesOrderHeader
     FOR JSON AUTO)  
```  
  
## Use FOR JSON output in SQL Server user-defined functions  
 You can create user-defined functions that format result sets as JSON and return this JSON output. The following example creates a user-defined function that fetches some sales order detail rows and formats them as a JSON array.  
  
```sql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
 RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
   RETURN (SELECT UnitPrice, OrderQty  
           FROM Sales.SalesOrderDetail  
           WHERE SalesOrderID = @salesOrderId  
           FOR JSON AUTO)  
END
```  
  
 You can use this function in a batch or query, as shown in the following example.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## Merge parent and child data into a single table  
In the following example, each set of child rows is formatted as a JSON array. The JSON array becomes the value of the Details column in the parent table.  
  
```sql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) AS Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## Update the data in JSON columns  
 The following example demonstrates that you can update the value of a column that contains JSON text.  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO) 
```  
  
## Use FOR JSON output in a C# client app  
 The following example shows how to retrieve the JSON output of a query into a StringBuilder object in a C# client app. Assume that the variable `queryWithForJson` contains the text of a SELECT statement with a FOR JSON clause.  
  
```csharp  
var queryWithForJson = "SELECT ... FOR JSON";
using(var conn = new SqlConnection("<connection string>"))
{
    using(var cmd = new SqlCommand(queryWithForJson, conn))
    {
        conn.Open();
        var jsonResult = new StringBuilder();
        var reader = cmd.ExecuteReader();
        if (!reader.HasRows)
        {
            jsonResult.Append("[]");
        }
        else
        {
            while (reader.Read())
            {
                jsonResult.Append(reader.GetValue(0).ToString());
            }
        }
    }
}
```  

## Learn more about JSON in SQL Server and Azure SQL Database  
  
### Microsoft videos

> [!NOTE]
> Some of the video links in this section may not work at this time. Microsoft is migrating content formerly on Channel 9 to a new platform. We will update the links as the videos are migrated to the new platform.

For a visual introduction to the built-in JSON support in SQL Server and Azure SQL Database, see the following videos:

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven-SQLServer2016/JSON-as-bridge-betwen-NoSQL-relational-worlds)
 
## See Also  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
