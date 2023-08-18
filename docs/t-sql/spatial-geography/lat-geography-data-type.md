---
title: "Lat (geography Data Type)"
description: "Lat (geography Data Type)"
author: MladjoA
ms.author: mlandzic
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "Lat"
  - "Lat_TSQL"
helpviewer_keywords:
  - "Lat method"
dev_langs:
  - "TSQL"
---
# Lat (geography Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  The latitude property of the **geography** instance.  
  
## Syntax  
  
```  
.Lat  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Return Types
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type: **float**  
  
 CLR type: **SqlDouble**  
  
## Remarks  
 In the OpenGIS model, Lat is defined only on **geography** instances composed of a single point. This property will return NULL if **geography** instances contain more than a single point. This property is precise and read-only.  
  
## Examples  
 This example creates a point and returns the latitude of the point.  
  
```sql
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## See Also  
 [Extended Methods on Geography Instances](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
