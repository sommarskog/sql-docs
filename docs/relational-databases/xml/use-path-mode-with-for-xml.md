---
title: "Use PATH Mode with FOR XML"
description: Learn how to use PATH mode with nested FOR XML queries and the TYPE directive to write less complex queries that return xml type instances.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 05/05/2022
ms.service: sql
ms.subservice: xml
ms.topic: conceptual
helpviewer_keywords:
  - "PATH FOR XML mode"
  - "characters [SQL Server], XML"
  - "aliases [SQL Server], XML"
  - "FOR XML clause, PATH mode"
  - "FOR XML PATH mode"
  - "column names [SQL Server]"
  - "XPath queries [SQL Server]"
---
# Use PATH mode with FOR XML

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

As described in [Constructing XML Using FOR XML](../../relational-databases/xml/for-xml-sql-server.md), the PATH mode provides a simpler way to mix elements and attributes. PATH mode is also a simpler way to introduce additional nesting for representing complex properties. You can use FOR XML EXPLICIT mode queries to construct such XML from a rowset, but the PATH mode provides a simpler alternative to the potentially cumbersome EXPLICIT mode queries. PATH mode, together with the ability to write nested FOR XML queries and the TYPE directive to return **xml** type instances, allows you to write queries with less complexity.

In PATH mode, column names or column aliases are treated as XPath expressions. These expressions indicate how the values are being mapped to XML. Each XPath expression is a relative XPath that provides the item type., such as the attribute, element, and scalar value, and the name and hierarchy of the node that will be generated relative to the row element.

This section describes mapping columns in a rowset under various conditions, and provides examples.

## In This Section

- [Columns without a Name](../../relational-databases/xml/columns-without-a-name.md)

- [Columns with a Name](../../relational-databases/xml/columns-with-a-name.md)

- [Columns with a Name Specified as a Wildcard Character](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)

- [Columns with the Name of an XPath Node Test](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)

- [Column Names with the Path Specified as data&#40;&#41;](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)

- [Columns that Contain a Null Value By Default](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)

- [Namespace Support in PATH Mode](../../relational-databases/xml/namespace-support-in-path-mode.md)

- [Examples: Using PATH Mode](../../relational-databases/xml/examples-using-path-mode.md)

## See also

- [Add Namespaces to Queries with WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)
