---
title: "Example: Specifying the ID and IDREFS Directives"
description: Learn how specifying the ID and IDREFS directives in an SQL query can enable intra-document links.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 05/05/2022
ms.service: sql
ms.subservice: xml
ms.topic: conceptual
helpviewer_keywords:
  - "IDREFS directive"
  - "ID directive"
---
# Example: Specify the ID and IDREFS directives

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

An element attribute can be specified as an **ID** type attribute, and the **IDREFS** attribute can then be used to refer to it. This enables intra-document links and is similar to the primary key and foreign key relationships in relational databases.

This example illustrates how the **ID** and **IDREFS** directives can be used to create attributes of **ID** and **IDREFS** types. Because IDs can't be integer values, the ID values in this example are converted. In other words, they're type casted. Prefixes are used for the ID values.

Assume that you want to construct XML as shown in the following:

```xml
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >
    <SalesOrder SalesOrderID="O11" OrderDate="..." />
    <SalesOrder SalesOrderID="O22" OrderDate="..." />
    <SalesOrder SalesOrderID="O33" OrderDate="..." />
    ...
</Customer>
```

The `SalesOrderIDList` attribute of the `<Customer>` element is a multivalued attribute that refers to the `SalesOrderID` attribute of the `<SalesOrder>` element. To establish this link, the `SalesOrderID` attribute must be declared of `ID` type, and the `SalesOrderIDList` attribute of the `<Customer>` element must be declared of `IDREFS` type. Because a customer can request several orders, the `IDREFS` type is used.

Elements of **IDREFS** type also have more than one value. Therefore, you have to use a separate select clause that will reuse the same tag, parent, and key column information. The `ORDER BY` then has to ensure that the sequence of rows that make up the **IDREFS** values appears grouped together under their parent element.

This is the query that produces the XML you want. The query uses the `ID` and `IDREFS` directives to overwrite the types in the column names (`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`).

```sql
USE AdventureWorks2022;
GO
SELECT  1 as Tag,
        0 as Parent,
        C.CustomerID   [Customer!1!CustomerID],
        NULL           [Customer!1!SalesOrderIDList!IDREFS],
        NULL           [SalesOrder!2!SalesOrderID!ID],
        NULL           [SalesOrder!2!OrderDate]
FROM   Sales.Customer C

UNION ALL
SELECT  1 as Tag,
        0 as Parent,
        C.CustomerID,
        'O-'+CAST(SalesOrderID as varchar(10)),
        NULL,
        NULL
FROM   Sales.Customer AS C
INNER JOIN Sales.SalesOrderHeader AS SOH
    ON  C.CustomerID = SOH.CustomerID

UNION ALL
SELECT 2 as Tag,
       1 as Parent,
        C.CustomerID,
        NULL,
        'O-'+CAST(SalesOrderID as varchar(10)),
        OrderDate
FROM   Sales.Customer AS C
INNER JOIN Sales.SalesOrderHeader AS SOH
    ON  C.CustomerID = SOH.CustomerID
ORDER BY [Customer!1!CustomerID] ,
         [SalesOrder!2!SalesOrderID!ID],
         [Customer!1!SalesOrderIDList!IDREFS]
FOR XML EXPLICIT;
```

## See also

- [Use EXPLICIT Mode with FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)
