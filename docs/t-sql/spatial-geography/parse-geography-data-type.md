---
title: "Parse (geography Data Type)"
description: "Parse (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "07/30/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
helpviewer_keywords:
  - "Parse method"
  - "Parse (geography Data Type)"
dev_langs:
  - "TSQL"
---
# Parse (geography Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Returns a **geography** instance from an Open Geospatial Consortium (OGC) Well-Known Text (WKT) representation. Parse() is equivalent to [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), except that it assumes a spatial reference ID (SRID) of 4326 as a parameter. The input may carry optional Z (elevation) and M (measure) values.
  
This **geography** data type method supports **FullGlobe** instances or spatial instances that are larger than a hemisphere.
  
## Syntax  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *geography_tagged_text*  
 Is the WKT representation of the **geography** instance to return. *geography_tagged_text* is an **nvarchar** expression.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geography**  
  
 CLR return type: **SqlGeography**  
  
## Remarks  
 The OGC type of the **geography** instance returned by `Parse()` is set to the corresponding WKT input.  
  
 The string 'Null' will be interpreted as a null **geography** instance.  
  
 This method will throw **ArgumentException** if the input contains an antipodal edge.  
  
## Examples  
 The following example uses `Parse()` to create a `geography` instance.  
  
```sql
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## See Also  
 [Extended Static Geography Methods](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;geography Data Type&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
