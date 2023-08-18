---
title: "STBoundary (geometry Data Type)"
description: "STBoundary (geometry Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STBoundary (geometry Data Type)"
  - "STBoundary_TSQL"
helpviewer_keywords:
  - "STBoundary (geometry Data Type)"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# STBoundary (geometry Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance FabricSE FabricDW](../../includes/applies-to-version/sql-asdb-asdbmi-fabricse-fabricdw.md)]

  Returns the boundary of a **geometry** instance.  
  
## Syntax  
  
```  
  
.STBoundary ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Return Types
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geometry**  
  
 CLR return type: **SqlGeometry**  
  
## Remarks  
 `STBoundary()` returns an empty **GeometryCollection** when the endpoints for a **LineString**, **CircularString**, or **CompoundCurve** instance are the same.  
  
## Examples  
  
### A. Using STBoundary() on a LineString instance with different endpoints  
 The following example creates a `LineString``geometry` instance. `STBoundary()` returns the boundary of the `LineString`.  
  
```sql
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STBoundary().ToString();  
```  
  
### B. Using STBoundary() on a LineString instance with the same endpoints  
 The following example creates a valid `LineString` instance with the same endpoints. `STBoundary()` returns an empty `GeometryCollection`.  
  
```sql
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, -2 2, 0 0)', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
### C. Using STBoundary() on a CurvePolygon instance  
 The following example uses `STBoundary()` on a `CurvePolygon` instance. `STBoundary()` returns a `CircularString` instance.  
  
```sql
 DECLARE @g geometry;  
 SET @g = geometry::STGeomFromText('CURVEPOLYGON(CIRCULARSTRING(0 0, 2 2, 0 2, -2 2, 0 0))', 0);  
 SELECT @g.STBoundary().ToString();
 ```  
  
## See Also  
 [OGC Methods on Geometry Instances](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
