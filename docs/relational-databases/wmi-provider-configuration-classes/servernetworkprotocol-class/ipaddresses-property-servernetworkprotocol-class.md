---
title: "IpAddresses Property (ServerNetworkProtocol)"
description: "IpAddresses Property (ServerNetworkProtocol Class)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "IpAddresses property"
apilocation: "sqlmgmproviderxpsp2up.mof"
apiname: "IpAddresses Property (ServerNetworkProtocol Class)"
apitype: "MOFDef"
---
# IpAddresses Property (ServerNetworkProtocol Class)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Gets the IP addresses associated with the server network protocol.  
  
## Syntax  
  
```  
  
object.IpAddresses [= value]  
```  
  
## Parts  
 *object*  
 A **ServerNetworkProtocol** object that represents the network protocol used by the instance of [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## Property Value/Return Value  
 An array of [ServerNetworkProtocolIPAdress Class](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) objects that represent the IP addresses supported by the server network protocol.  
  
## Remarks  
  
## See Also  
 [Configuring Server Network Protocols and Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
