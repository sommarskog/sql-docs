---
title: "Updating Data"
description: "Updating Data"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: conceptual
helpviewer_keywords:
  - "data updates [ADO], about data updates"
  - "updating data [ADO], about updating data"
---
# Updating Data
Update behavior and functionality is largely dependent upon update mode (lock type), cursor type, and cursor location.  
  
 Use the **Update** method to save any changes you have made to the current record of a **Recordset** object since calling the **AddNew** method or since changing any field values in an existing record. The **Recordset** object must support updates.  
  
 If the **Recordset** object supports batch updating, you can cache multiple changes to one or more records locally until you call the **UpdateBatch** method. If you are editing the current record or adding a new record when you call the **UpdateBatch** method, ADO will automatically call the **Update** method to save any pending changes to the current record before transmitting the batched changes to the provider.  
  
 The current record remains current after you call the **Update** or **UpdateBatch** methods.  
  
 This section contains the following topics.  
  
-   [Immediate Mode](../../../ado/guide/data/immediate-mode.md)  
  
-   [Batch Mode](../../../ado/guide/data/batch-mode.md)  
  
-   [Transaction Processing](../../../ado/guide/data/transaction-processing.md)
