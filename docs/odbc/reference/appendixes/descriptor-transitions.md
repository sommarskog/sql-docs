---
title: "Descriptor Transitions"
description: "Descriptor Transitions"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "state transitions [ODBC], descriptor"
  - "transitioning states [ODBC], descriptor"
  - "descriptor transitions [ODBC]"
---
# Descriptor Transitions
ODBC descriptors have the following three states.  
  
|State|Description|  
|-----------|-----------------|  
|D0|Unallocated descriptor|  
|D1i|Implicitly allocated descriptor|  
|D1e|Explicitly allocated descriptor|  
  
 The following tables show how each ODBC function affects the descriptor state.  
  
## SQLAllocHandle  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1]   This row shows transitions when *HandleType* was SQL_HANDLE_STMT.  
  
 [2]   This row shows transitions when *HandleType* was SQL_HANDLE_DESC.  
  
## SQLCopyDesc  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## SQLFreeHandle  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1]   This row shows transitions when *HandleType* was SQL_HANDLE_STMT.  
  
 [2]   This row shows transitions when *HandleType* was SQL_HANDLE_DESC.  
  
## SQLGetDescField and SQLGetDescRec  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## SQLSetDescField and SQLSetDescRec  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)[1]|--|--|  
  
 [1]   This row shows transitions when *DescriptorHandle* was the handle of an ARD, APD, or IPD, or (for **SQLSetDescField**) when *DescriptorHandle* was the handle of an IRD and *FieldIdentifier* was SQL_DESC_ARRAY_STATUS_PTR or SQL_DESC_ROWS_PROCESSED_PTR.  
  
## All Other ODBC Functions  
  
|D0<br /><br /> Unallocated|D1i<br /><br /> Implicit|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--|--|--|
