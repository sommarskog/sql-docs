---
title: "STBuffer (geography Data Type)"
description: "STBuffer (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STBuffer (geography Data Type)"
  - "STBuffer_TSQL"
helpviewer_keywords:
  - "STBuffer (geography Data Type)"
dev_langs:
  - "TSQL"
---
# STBuffer (geography Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns a geography object that represents the union of all points whose distance from a **geography** instance is less than or equal to a specified value.  
  
 This geography data type method supports **FullGlobe** instances or spatial instances that are larger than a hemisphere.  
  
## Syntax  
  
```  
  
.STBuffer ( distance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *distance*  
 Is a value of type **float** (**double** in the .NET Framework) specifying the distance from the **geography** instance around which to calculate the buffer.  
  
 The maximum distance of the buffer cannot exceed 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 Earth's circumference) or the full globe.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geography**  
  
 CLR return type: **SqlGeography**  
  
## Remarks  
 STBuffer() calculates a buffer in the same manner as [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md), specifying *tolerance* = abs(distance) \* .001 and *relative* = **false**.  
  
 A negative buffer removes all points within the given distance of the boundary of the **geography** instance.  
  
 `STBuffer()` will return a **FullGlobe** instance in certain cases; for example, `STBuffer()` returns a **FullGlobe** instance when the buffer distance is greater than the distance from the equator to the poles. A buffer cannot exceed the full globe.  
  
 This method will throw an **ArgumentException** in **FullGlobe** instances where the distance of the buffer exceeds the following limitation:  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 1/2 Earth's circumference)  
  
 The maximum distance limit allows the construction of the buffer to be as flexible as possible.  
  
 The error between the theoretical and computed buffer is max(tolerance, extents * 1.E-7) where tolerance = distance \* .001. For more information on extents, see [geography Data Type Method Reference](./stequals-geography-data-type.md).  
  
## Examples  
 The following example creates a `LineString``geography` instance. It then uses `STBuffer()` to return the region within 1 meter of the instance.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## See Also  
 [BufferWithTolerance &#40;geography Data Type&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [OGC Methods on Geography Instances](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
