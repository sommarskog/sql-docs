---
title: "Open Method (ADO MD)"
description: "Open Method (ADO MD)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
helpviewer_keywords:
  - "Open method [ADO MD]"
apitype: "COM"
---
# Open Method (ADO MD)
Retrieves the results of a multidimensional query and returns the results to a [Cellset](./cellset-object-ado-md.md).  
  
## Syntax  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### Parameters  
 *Source*  
 Optional. A **Variant** that evaluates to a valid multidimensional query, such as a Multidimensional Expression (MDX) query. The *Source* argument corresponds to the [Source](./source-property-ado-md.md) property. For more information about MDX, see the [OLE DB for Online Analytical Processing (OLAP)](/previous-versions/windows/desktop/ms717005(v=vs.85)) documentation in the Microsoft Data Access Components SDK.  
  
 *ActiveConnection*  
 Optional. A **Variant** that evaluates to a string specifying either a valid ADO [Connection](../ado-api/connection-object-ado.md) object variable name or a definition for a connection. The *ActiveConnection* argument specifies the connection in which to open the [Cellset](./cellset-object-ado-md.md) object. If you pass a connection definition for this argument, ADO opens a new connection using the specified parameters. The *ActiveConnection* argument corresponds to the [ActiveConnection](./activeconnection-property-ado-md.md) property.  
  
## Remarks  
 The **Open** method generates an error if either of its parameters is omitted and its corresponding property value has not been set prior to attempting to open the **Cellset**.  
  
## Applies To  
 [Cellset Object (ADO MD)](./cellset-object-ado-md.md)  
  
## See Also  
 [Cellset Example (VB)](./cellset-example-vb.md)   
 [ActiveConnection Property (ADO MD)](./activeconnection-property-ado-md.md)   
 [Close Method (ADO MD)](./close-method-ado-md.md)   
 [Connection Object (ADO)](../ado-api/connection-object-ado.md)   
 [Source Property (ADO MD)](./source-property-ado-md.md)   
 [State Property (ADO MD)](./state-property-ado-md.md)