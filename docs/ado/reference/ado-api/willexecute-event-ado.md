---
title: "WillExecute Event (ADO)"
description: "WillExecute Event (ADO)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
f1_keywords:
  - "WillExecute"
  - "Connection::WillExecute"
helpviewer_keywords:
  - "WillExecute event [ADO]"
apitype: "COM"
---
# WillExecute Event (ADO)
The **WillExecute** event is called just before a pending command executes on a connection.  
  
## Syntax  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### Parameters  
 *Source*  
 A **String** that contains an SQL command or a stored procedure name.  
  
 *CursorType*  
 A [CursorTypeEnum](./cursortypeenum.md) that contains the type of cursor for the **Recordset** that will be opened. With this parameter, you can change the cursor to any type during a **Recordset**[Open Method (ADO Recordset)](./open-method-ado-recordset.md) operation. *CursorType* will be ignored for any other operation.  
  
 *LockType*  
 A [LockTypeEnum](./locktypeenum.md) that contains the lock type for the **Recordset** that will be opened. With this parameter, you can change the lock to any type during a **RecordsetOpen** operation. *LockType* will be ignored for any other operation.  
  
 *Options*  
 A **Long** value that indicates options that can be used to execute the command or open the **Recordset**.  
  
 *adStatus*  
 An [EventStatusEnum](./eventstatusenum.md) status value that may be **adStatusCantDeny** or **adStatusOK** when this event is called. If it is **adStatusCantDeny**, this event may not request cancellation of the pending operation.  
  
 *pCommand*  
 The [Command Object (ADO)](./command-object-ado.md) object for which this event notification applies.  
  
 *pRecordset*  
 The [Recordset Object (ADO)](./recordset-object-ado.md) object for which this event notification applies.  
  
 *pConnection*  
 The [Connection Object (ADO)](./connection-object-ado.md) object for which this event notification applies.  
  
## Remarks  
 A **WillExecute** event may occur due to a Connection.  [Execute Method (ADO Connection)](./execute-method-ado-connection.md), [Execute Method (ADO Command)](./execute-method-ado-command.md), or [Open Method (ADO Recordset)](./open-method-ado-recordset.md) method The *pConnection* parameter should always contain a valid reference to a **Connection** object. If the event is due to **Connection.Execute**, the *pRecordset* and *pCommand* parameters are set to **Nothing**. If the event is due to **Recordset.Open**, the *pRecordset* parameter will reference the **Recordset** object and the *pCommand* parameter is set to **Nothing**. If the event is due to **Command.Execute**, the *pCommand* parameter will reference the **Command** object and the *pRecordset* parameter is set to **Nothing**.  
  
 **WillExecute** allows you to examine and modify the pending execution parameters. This event may return a request that the pending command be canceled.  
  
> [!NOTE]
>  If the original source for a **Command** is a stream specified by the [CommandStream Property (ADO)](./commandstream-property-ado.md) property, assigning a new string to the **WillExecute**_Source_ parameter changes the source of the **Command**. The **CommandStream** property will be cleared and the [CommandText Property (ADO)](./commandtext-property-ado.md) property will be updated with the new source. The original stream specified by **CommandStream** will be released and cannot be accessed.  
  
 If the dialect of the new source string differs from the original setting of the [Dialect Property](./dialect-property.md) property (which corresponded to the **CommandStream**), the correct dialect must be specified by setting the **Dialect** property of the command object referenced by *pCommand*.  
  
## See Also  
 [ADO Events Model Example (VC++)](./ado-events-model-example-vc.md)   
 [ADO Event Handler Summary](../../guide/data/ado-event-handler-summary.md)   
 [Connection Object (ADO)](./connection-object-ado.md)