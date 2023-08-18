---
title: "SetOrderValue Method (ClientNetworkProtocol)"
description: "SetOrderValue Method (ClientNetworkProtocol Class)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "SetOrderValue method"
apilocation: "sqlmgmproviderxpsp2up.mof"
apiname: "SetOrderValue Method (ClientNetworkProtocol Class)"
apitype: "MOFDef"
---
# SetOrderValue Method (ClientNetworkProtocol Class)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Selects the protocol with the specified order value from the client protocol list.  
  
## Syntax  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## Parts  
 *object*  
 A [ClientNetworkProtocol Class](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) object that represents the network protocol used by the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] client.  
  
#### Parameters  
  
|Parameter|Description|  
|---------------|-----------------|  
|*OrderValue*|A u**int32** value that sets the order value.|  
  
## Property Value/Return Value  
 A **uint32** value, which is 0 if the service was successfully modified, 1 if the request is not supported, and any other number to indicate an error.  
  
## Remarks  
  
## See Also  
 [Client Protocols Properties (Order Tab)](../../../tools/configuration-manager/client-protocols-properties-order-tab.md)  
  
