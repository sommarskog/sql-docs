---
title: "STMPolyFromWKB (geography Data Type)"
description: "STMPolyFromWKB (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "07/30/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "STMPolyFromWKB (geography Data Type)"
  - "STMPolyFromWKB_TSQL"
helpviewer_keywords:
  - "STMPolyFromWKB method"
dev_langs:
  - "TSQL"
---
# STMPolyFromWKB (geography Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Returns a **geographyMultiPolygon** instance from an Open Geospatial Consortium (OGC) Well-Known Binary (WKB) representation.
  
## Syntax  
  
```  
  
STMPolyFromWKB ( 'WKB_multipolygon' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *WKB_multipolygon*  
 Is the WKB representation of the **geographyMultiPolygon** instance you wish to return. *WKB_multipolygon* is a **varbinary(max)** expression.  
  
 *SRID*  
 Is an **int** expression representing the spatial reference ID (SRID) of the **geographyMultiPolygon** instance you wish to return.  
  
## Return Types  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] return type: **geography**  
  
 CLR return type: **SqlGeography**  
  
 OGC type: **MultiPolygon**  
  
## Examples  
 The following example uses `STMPolyFromWKB()` to create a `geography` instance.  
  
```sql
DECLARE @g geography;  
SET @g = geography::STMPolyFromWKB(0x01060000000200000001030000000100000004000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D34740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D3474001030000000100000004000000E7FBA9F1D2955EC08716D9CEF7D34740E7FBA9F1D2955EC0F853E3A59BD447405839B4C876965EC0F853E3A59BD44740E7FBA9F1D2955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## See Also  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
