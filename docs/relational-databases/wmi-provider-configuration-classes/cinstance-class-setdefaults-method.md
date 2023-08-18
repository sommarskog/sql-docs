---
title: "SetDefaults Method (CInstance)"
description: "CInstance Class - SetDefaults Method"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "SetDefaults method"
apilocation: "sqlmgmproviderxpsp2up.mof"
apiname: "SetDefaults Method (CInstance Class)"
apitype: "MOFDef"
---
# CInstance Class - SetDefaults Method
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Sets all the default values for the instance of the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client with the option to overwrite existing data.  
  
## Syntax  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## Parts  
 *object*  
 A [CInstance Class](../../relational-databases/wmi-provider-configuration-classes/cinstance-class.md) object that represents a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client instance.  
  
#### Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|*OverwriteAll*|A Boolean value that specifies whether to overwrite existing values on the instance of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client: **true** to overwrite existing data, or **false** if existing data is not to be overwritten.|  
  
## Property Value/Return Value  
 A **uint32** value, which is 0 if the service was successfully modified, 1 if the request is not supported, and any other number to indicate an error.  
  
## Remarks  
  
## See Also  
 [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)  
  
