---
title: Reduce (geography Data Type)
description: "Reduce (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "Reduce_TSQL"
  - "Reduce"
helpviewer_keywords:
  - "Reduce method"
dev_langs:
  - "TSQL"
---
# Reduce (geography Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns an approximation of the given **geography** instance produced by running the Douglas-Peucker algorithm on the instance with the given tolerance.  
  
 This **geography** data type method supports **FullGlobe** instances or spatial instances that are larger than a hemisphere.  
  
## Syntax  
  
```  
  
.Reduce ( tolerance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

|Term|Definition|
|----|----------|
|*tolerance*|Is a value of type **float**. *tolerance* is the tolerance to input to the Douglas-Peucker algorithm. *tolerance* must be a positive number.|  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geography**  
  
 CLR return type: **SqlGeography**  
  
## Remarks  
 For collection types, this algorithm operates independently on each **geography** contained in the instance. This algorithm does not modify **Point** instances.  
  
 This method will attempt to preserve the endpoints of **LineString** instances, but may fail to do so in order to preserve a valid result.  
  
 If `Reduce()` is called with a negative value, this method will produce an **ArgumentException**. Tolerances used in `Reduce()` must be positive numbers.  
  
 The Douglas-Peucker algorithm works on each curve or ring in the **geography** instance by removing all points except for the start point and end point. Each point removed is then added back, starting with the farthest outlying point, until no point is more than *tolerance* from the result. The result is then made valid if necessary, as a valid result is guaranteed.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], this method has been extended to **FullGlobe** instances.  
  
 This method is not precise.  
  
## Examples  
 The following example creates a `LineString` instance and uses `Reduce()` to simplify the instance.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## See Also  
 [Extended Methods on Geography Instances](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
