---
title: GeomFromGML (geography Data Type)
description: "GeomFromGML (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "07/30/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "GeomFromGML_TSQL"
  - "GeomFromGML"
helpviewer_keywords:
  - "GeomFromGML (geography Data Type)"
  - "GeomFromGML method"
dev_langs:
  - "TSQL"
---

# GeomFromGML (geography Data Type)

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Constructs a **geography** instance given a representation in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subset of the Geography Markup Language (GML).
  
For more information on GML, see the following Open Geospatial Consortium Specifications: [OGC Specifications, Geography Markup Language](https://go.microsoft.com/fwlink/?LinkId=93629)
  
This **geography** data type method supports **FullGlobe** instances or spatial instances that are larger than a hemisphere.
  
## Syntax  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *GML_input*  
 Is an XML input from which the GML will return a value.  
  
 *SRID*  
 Is an **int** expression representing the spatial reference ID (SRID) of the **geography** instance to return.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geography**  
  
 CLR return type: **SqlGeography**  
  
## Remarks  
 This method throws a **FormatException** if the input is not well-formatted.  
  
 This method will throw **ArgumentException** if the input contains antipodal edge.  
  
## Examples  
 The following example uses `GeomFromGml()` to create a `geography` instance.  
  
```sql
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
 The following example uses `GeomFromGml()` to create a `FullGlobe``geography` instance.  
  
```sql
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<FullGlobe xmlns="http://schemas.microsoft.com/sqlserver/2011/geography" />';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
## See Also  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
