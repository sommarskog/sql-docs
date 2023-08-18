---
title: "sys.spatial_indexes (Transact-SQL)"
description: sys.spatial_indexes (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.spatial_indexes_TSQL"
  - "spatial_indexes"
  - "spatial_indexes_TSQL"
  - "sys.spatial_indexes"
helpviewer_keywords:
  - "sys.spatial_indexes catalog view"
dev_langs:
  - "TSQL"
---
# sys.spatial_indexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Represents the main index information of the spatial indexes.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||Inherits columns from [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|spatial_index_type|**tinyint**|Type of spatial index:<br /><br /> 1 = Geometric spatial index<br /><br /> 2 = Geographic spatial index|  
|spatial_index_type_desc|**nvarchar(60)**|Type description of spatial index:<br /><br /> GEOMETRY = geometric spatial index<br /><br /> GEOGRAPHY = geographic spatial index|  
|tessellation_scheme|**sysname**|Name of tessellation scheme:<br /><br /> GEOMETRY_GRID, GEOMETRY_AUTO_GRID,<br /><br /> GEOGRAPHY_GRID, GEOGRAPHY_AUTO_GRID<br /><br /> Note: For information about tessellation schemes, see [Spatial Indexes Overview](../../relational-databases/spatial/spatial-indexes-overview.md).|  
|\<inherited columns>||Inherits columns from [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).<br /><br /> The inherited columns has_filter and filter_definition appear after the columns that are specific to spatial indexes.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## See Also  
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Spatial Indexes Overview](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
