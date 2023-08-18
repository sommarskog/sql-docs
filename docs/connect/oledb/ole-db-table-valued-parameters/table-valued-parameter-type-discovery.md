---
title: Table-valued parameter type discovery (OLE DB driver)
description: Learn how a consumer can discover the metadata information for each individual column of the table-valued parameter in OLE DB Driver for SQL Server.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "table-valued parameters, type discovery"
---
# Table-Valued Parameter Type Discovery (OLE DB driver)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  The consumer-that is, the client application using the OLE DB Driver for SQL Server-can discover the type of each command parameter if the command text has been given to the OLE DB Provider. After the type of a table-valued parameter is known, the consumer can discover the metadata information for each individual column of the table-valued parameter.  
  
 The type information of procedure parameters is supported by ICommandWithParameters::GetParameterInfo for most parameter types. Beginning with [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], with the introduction of user-defined types and the **xml** data type, the GetParameterInfo method was not sufficient for this purpose because it was not possible to provide user-defined type information (name, schema, and catalog) through ICommandWithParameters. A new interface, ISSCommandWithParameters, was defined to provide extended type information.  
  
 For table-valued parameters, you also use the ISSCommandWithParameters interface to discover detailed information. The client calls ISSCommandWithParameters::GetParameterInfo after preparing the command object. For table-valued parameters, the *wType* member of the DBPARAMINFO structure is set to DBTYPE_TABLE by the provider. The *ulParamSize* field of DBPARAMINFO structure has a value of ~0.  
  
 The consumer would then request additional properties (table-valued parameter type catalog name, table-valued parameter type schema name, table-valued parameter type name, column ordering, and default columns) by using ISSCommandWithParameters::GetParameterProperties.  
  
 After the type name is known, to retrieve the individual column information the consumer must either call IOpenRowset::OpenRowsetor obtain the DBSCHEMA_TABLE_TYPE_COLUMNS rowset by specifying the table-valued parameter type name as the table name.  
  
## See Also  
 [Table-Valued Parameters &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Use Table-Valued Parameters &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
