---
title: "GetNextOrderValue Method (ClientNetworkProtocol)"
description: "GetNextOrderValue Method (ClientNetworkProtocol Class)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "GetNextOrderValue method"
apilocation: "sqlmgmproviderxpsp2up.mof"
apiname: "GetNextOrderValue Method (ClientNetworkProtocol Class)"
apitype: "MOFDef"
---
# GetNextOrderValue Method (ClientNetworkProtocol Class)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Selects the protocol that is in the next position in the list of protocols.  
  
## Syntax  
  
```  
  
object.GetNextOrderValue()  
```  
  
## Parts  
 *object*  
 A [ClientNetworkProtocol Class](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) object that represents the network protocol used by the [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
## Property Value/Return Value  
 A **uint32** value, which is 0 if the service was successfully modified, 1 if the request is not supported, and any other number to indicate an error.  
  
## Remarks  
  
## See Also  
 [Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)   
 [Configuring Client Network Protocols and Net-Libraries](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
