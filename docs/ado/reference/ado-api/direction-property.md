---
title: "Direction Property"
description: "Direction Property"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
f1_keywords:
  - "_Parameter::Direction"
helpviewer_keywords:
  - "Direction property"
apitype: "COM"
---
# Direction Property
Indicates whether the [parameter](../../../ado/reference/ado-api/parameter-object.md) represents an input parameter, an output parameter, an input and an output parameter, or if the parameter is the return value from a stored procedure.  
  
## Settings and Return Values  
 Sets or returns a [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) value.  
  
## Remarks  
 Use the **Direction** property to specify how a parameter is passed to or from a procedure. The **Direction** property is read/write; this allows you to work with providers that don't return this information or to set this information when you don't want ADO to make an extra call to the provider to retrieve parameter information.  
  
 Not all providers can determine the direction of parameters in their stored procedures. In these cases, you must set the **Direction** property before you execute the query.  
  
## Applies To  
 [Parameter Object](../../../ado/reference/ado-api/parameter-object.md)  
  
## See Also  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size, and Direction Properties Example (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size, and Direction Properties Example (VC++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size, and Direction Properties Example (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
