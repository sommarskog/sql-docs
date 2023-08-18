---
title: "MSSQLSERVER_7915"
description: "MSSQLSERVER_7915"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "7915 (Database Engine error)"
---
# MSSQLSERVER_7915
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|7915|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Message Text|Repair: IAM chain for object ID O_ID, index ID I_ID, partition ID PN_ID, alloc unit ID A_ID (type TYPE), has been truncated before page P_ID and will be rebuilt.|  
  
## Explanation  
This is an information message sent by REPAIR that indicates that the specified Index Allocation Map (IAM) chain was patched so that it could be rebuilt. This patching may have required the allocation of a new head of the IAM chain or the removal of bad pages from the chain.  
  
## User Action  
None  
  
