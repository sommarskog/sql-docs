---
title: "Large CLR User-Defined Types"
description: Learn about size restrictions and related behavior for user-defined types in the common language runtime for different versions of SQL Server.
author: David-Engel
ms.author: v-davidengel
ms.date: "06/12/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
helpviewer_keywords:
  - "large CLR user-defined types"
---
# Large CLR User-Defined Types
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  In SQL Server 2005, user-defined types (UDTs) in the common language runtime (CLR) were restricted to 8,000 bytes in size. This restriction has been lifted in [!INCLUDE[sql2008-md](../../../includes/sql2008-md.md)] and later versions. CLR UDTs are now treated in a similar way to large object (LOB) types. That is, UDTs less than or equal to 8,000 bytes behave the same way as in SQL Server 2005, but larger UDTs are supported and report their size as "unlimited".  
  
 For more information, see [Large CLR User-Defined Types &#40;OLE DB&#41;](../../oledb/ole-db/large-clr-user-defined-types-ole-db.md).  
  
## Use Cases   
  
 For OLE DB, support for large UDTs includes the ability to stream UDT values to and from the server by using ISequentialStream binding.  
  
 UDTs less than or equal to 8,000 bytes will behave as they did in SQL Server 2005. For OLE DB, you can still stream small UDTs by using ISequentialStream binding.  
  
 Sometimes native code will have to understand the contents of CLR UDTs, but will not have to instantiate managed objects. If this is the case, you can use custom serialization to convert UDT values on the server into a well known format for clients.  
  
 For applications that have existing data access code, you can exploit CLR UDT behavior on the client by retrieving UDTs through native APIs and instantiating them by using C++ CLI interop in mixed mode applications.  
  
## See Also  
 [OLE DB Driver for SQL Server Features](../../oledb/features/oledb-driver-for-sql-server-features.md)    
  
  
