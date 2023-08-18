---
title: "Copying Descriptors"
description: "Copying Descriptors"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "descriptors [ODBC], copying"
  - "copying descriptors [ODBC]"
---
# Copying Descriptors
The **SQLCopyDesc** function is called to copy the fields of one descriptor to another descriptor. Fields can be copied only to an application descriptor or an IPD, but not to an IRD. Fields can be copied from any type of descriptor. Only those fields that are defined for both the source and target descriptors are copied. **SQLCopyDesc** does not copy the SQL_DESC_ALLOC_TYPE field, because a descriptor's allocation type cannot be changed. Copied fields overwrite the existing fields.  
  
 An ARD on one statement handle can serve as the APD on another statement handle. This allows an application to copy rows between tables without copying data at the application level. To do this, a row descriptor that describes a fetched row of a table is reused as a parameter descriptor for a parameter in an INSERT statement. The SQL_MAX_CONCURRENT_ACTIVITIES information type must be greater than 1 for this operation to succeed.
