---
title: "Schema Rowsets Changed for OLE DB Table-Valued Parameters"
description: Learn about the schema rowsets that have been changed or added to support table-valued parameters in OLE DB Driver for SQL Server.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "schema rowsets [OLE DB]"
  - "table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)"
---
# Schema Rowsets Changed for OLE DB Table-Valued Parameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  The following are the schema rowsets that have been changed or added to support table-valued parameters.  
  
|Schema rowset|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Two new columns were added at the end of the rowset named SS_TYPE_CATALOG_NAME and SS_TYPE_SCHEMANAME. These columns could be re-used for future types. The TYPE_NAME and LOCAL_TYPE_NAME columns will contain the name of the table-valued parameter TABLE type. The DATA_TYPE column will have value DBTYPE_TABLE = 143 for table-valued parameters.|  
|DBSCHEMA_TABLE_TYPES|This rowset was added to support table-valued parameters. It is identical to DBSCHEMA_TABLES, except that it returns metadata only for table types, rather than for tables, views, or synonyms. The TABLE_TYPE column will have the value 'TABLE TYPE'.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|This rowset was added to support table-valued parameters. It is identical to DBSCHEMA_PRIMARY_KEYS, except that it returns primary keys metadata only for table types, rather than for tables.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|This rowset was added to support table-valued parameters. It is identical to DBSCHEMA_COLUMNS, except that it returns column metadata only for table types, rather than for tables, views, or synonyms.|  
  
## See Also  
 [Table-Valued Parameters &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Use Table-Valued Parameters &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
