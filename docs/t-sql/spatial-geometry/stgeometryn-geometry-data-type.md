---
title: "STGeometryN (geometry Data Type)"
description: "STGeometryN (geometry Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "08/03/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STGeometryN_TSQL"
  - "STGeometryN (geometry Data Type)"
helpviewer_keywords:
  - "STGeometryN (geometry Data Type)"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# STGeometryN (geometry Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance FabricSE FabricDW](../../includes/applies-to-version/sql-asdb-asdbmi-fabricse-fabricdw.md)]

Returns a specified geometry in a **geometry collection**.
  
## Syntax  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *expression*  
 Is an **int** expression between 1 and the number of **geometry** instances in the **geometrycollection**.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geometry**  
  
 CLR return type: **SqlGeometry**  
  
## Remarks  
 This method returns **null** if the parameter is larger than the result of `STNumGeometries()` and will throw an **ArgumentOutOfRangeException** if the *expression* parameter is less than 1.  
  
## Examples  
 The following example creates a `MultiPoint``geometry collection` and uses `STGeometryN()` to find the second `geometry` instance of the collection.  
  
```sql
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT(0 0, 13.5 2, 7 19)', 0);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## See Also  
 [OGC Methods on Geometry Instances](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

