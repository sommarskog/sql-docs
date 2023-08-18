---
title: "CacheSize Property (ADO)"
description: "CacheSize Property (ADO)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
f1_keywords:
  - "Recordset15::CacheSize"
helpviewer_keywords:
  - "CacheSize property [ADO]"
apitype: "COM"
---
# CacheSize Property (ADO)
Indicates the number of records from a [Recordset](./recordset-object-ado.md) object that are cached locally in memory.  
  
## Settings and Return Values  
 Sets or returns a **Long** value that must be greater than 0. Default is 1.  
  
## Remarks  
 Use the **CacheSize** property to control how many records to retrieve at one time into local memory from the provider. For example, if the **CacheSize** is 10, after first opening the **Recordset** object, the provider retrieves the first 10 records into local memory. As you move through the **Recordset** object, the provider returns the data from the local memory buffer. As soon as you move past the last record in the cache, the provider retrieves the next 10 records from the data source into the cache.  
  
> [!NOTE]
>  **CacheSize** is based on the **Maximum Open Rows** provider-specific property (in the **Properties** collection of the **Recordset** object). You cannot set **CacheSize** to a value greater than **Maximum Open Rows**. To modify the number of rows which can be opened by the provider, set **Maximum Open Rows**.  
  
 The value of **CacheSize** can be adjusted during the life of the **Recordset** object, but changing this value only affects the number of records in the cache after subsequent retrievals from the data source. Changing the property value alone will not change the current contents of the cache.  
  
 If there are fewer records to retrieve than **CacheSize** specifies, the provider returns the remaining records and no error occurs.  
  
 A **CacheSize** setting of zero is not allowed and returns an error.  
  
 Records retrieved from the cache don't reflect concurrent changes that other users made to the source data. To force an update of all the cached data, use the [Resync](./resync-method.md) method.  
  
 If **CacheSize** is set to a value greater than one, the navigation methods ([Move](./move-method-ado.md), [MoveFirst, MoveLast, MoveNext, and MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) may result in navigation to a deleted record, if deletion occurs after the records were retrieved. After the initial fetch, subsequent deletions will not be reflected in your data cache until you attempt to access a data value from a deleted row. However, setting **CacheSize** to one eliminates this issue since deleted rows cannot be fetched.  
  
## Applies To  
 [Recordset Object (ADO)](./recordset-object-ado.md)  
  
## See Also  
 [CacheSize Property Example (VB)](./cachesize-property-example-vb.md)   
 [CacheSize Property Example (VC++)](./cachesize-property-example-vc.md)   
 [CacheSize Property Example (JScript)](./cachesize-property-example-jscript.md)