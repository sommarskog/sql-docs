---
title: "STEquals (geometry Data Type)"
description: "STEquals (geometry Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "08/03/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STEquals (geometry Data Type)"
  - "STEquals_TSQL"
helpviewer_keywords:
  - "STEquals (geometry Data Type)"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# STEquals (geometry Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance FabricSE FabricDW](../../includes/applies-to-version/sql-asdb-asdbmi-fabricse-fabricdw.md)]

Returns 1 if a **geometry** instance represents the same point set as another **geometry** instance. Returns 0 if it does not.
  
## Syntax  
  
```  
  
.STEquals ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *other_geometry*  
 Is another **geometry** instance to compare against the instance on which `STEquals()` is invoked.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **bit**  
  
 CLR return type: **SqlBoolean**  
  
## Remarks  
 This method always returns null if the spatial reference IDs (SRIDs) of the **geometry** instances do not match.  
  
## Examples  
 The following example creates two `geometry` instances with `STGeomFromText()` that are equal but not trivially equal, and uses `STEquals()` to test their equality.  
  
```  
DECLARE @g geometry  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('MULTILINESTRING((4 2, 2 0), (0 2, 2 0))', 0);  
SELECT @g.STEquals(@h);  
```  
  
## See Also  
 [Spatial Indexes Overview](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [OGC Methods on Geometry Instances](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

