---
title: "STNumGeometries (geometry Data Type)"
description: "STNumGeometries (geometry Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "08/03/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STNumGeometries (geometry Data Type)"
  - "STNumGeometries_TSQL"
helpviewer_keywords:
  - "STNumGeometries (geometry Data Type)"
dev_langs:
  - "TSQL"
---
# STNumGeometries (geometry Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Returns the number of geometries that comprise a **geometry** instance.
  
## Syntax  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Return Types
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **int**  
  
 CLR return type: **SqlInt32**  
  
## Remarks  
 This method returns 1 if the **geometry** instance is not a **MultiPoint**, **MultiLineString**, **MultiPolygon**, or **GeometryCollection** instance, and 0 if the **geometry** instance is empty.  
  
> [!NOTE]  
>  If a **GeometryCollection** has nested empty elements, `STNumGeometries()` will not return 0. Though the elements in the **GeometryCollection** instance are empty, the instance itself is not an empty set.  
  
  

