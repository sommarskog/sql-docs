---
title: "Columns with the Name of an XPath Node Test"
description: Learn how XML content is mapped when an SQL query contains columns with the name of an XPath node test, such as text() or comment().
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 05/05/2022
ms.service: sql
ms.subservice: xml
ms.topic: conceptual
helpviewer_keywords:
  - "names [SQL Server], columns with"
  - "XPath node test"
---
# Columns with the name of an XPath node test

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

If the column name is one of the XPath node tests, the content is mapped as shown in the following table. When the column name is an XPath node test, the content is mapped to the corresponding node. If the SQL type of the column is **xml**, an error is returned.

|Column Name|Behavior|
|-----------------|--------------|
|text()|For a column with the name of text(), the string value in that column is added as a text node.|
|comment()|For a column with the name of comment(), the string value in that column is added as an XML comment.|
|node()|For a column with the name of node(), the result is the same as when the column name is a wildcard character (`*`).|
|processing-instruction(name)|For a column with the name of a processing instruction, the string value in that column is added as the PI value for the processing instruction target name.|

The following query shows the use of the node tests as column names. It adds text nodes and comments in the resulting XML.

```sql
USE AdventureWorks2022;
GO
SELECT E.BusinessEntityID "@EmpID",
        'Example of using node tests such as text(), comment(), processing-instruction()'  as "comment()",
        'Some PI'                        as "processing-instruction(PI)",
        'Employee name and address data' as "text()",
        'middle name is optional'        as "EmpName/text()",
        FirstName                        as "EmpName/First",
        MiddleName                       as "EmpName/Middle",
        LastName                         as "EmpName/Last",
        AddressLine1                     as "Address/AddrLine1",
        AddressLine2                     as "Address/AddrLIne2",
        City                             as "Address/City"
FROM   HumanResources.Employee AS E
INNER JOIN Person.Person AS P
    ON P.BusinessEntityID = E.BusinessEntityID
INNER JOIN Person.BusinessEntityAddress AS BAE
    ON BAE.BusinessEntityID = E.BusinessEntityID
INNER JOIN Person.Address AS A
    ON BAE.AddressID = A.AddressID
WHERE  E.BusinessEntityID=1
FOR XML PATH;
```

This is the result:

```xml

<row EmpID="1">
<!--Example of using node tests such as text(), comment(), processing-instruction() -->
<?PI Some PI?>
    Employee name and address data
    <EmpName>middle name is optional
        <First>Ken</First>
        <Last>Sánchez</Last>
    </EmpName>
    <Address>
        <AddrLine1>4350 Minute Dr.</AddrLine1>
        <City>Minneapolis</City>
    </Address>
</row>
```

## See also

- [Use PATH Mode with FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)
