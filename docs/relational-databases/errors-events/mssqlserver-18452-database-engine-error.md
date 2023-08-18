---
title: "MSSQLSERVER_18452"
description: "MSSQLSERVER_18452"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "18456 (Database Engine error)"
  - "18452 (Database Engine error)"
---
# MSSQLSERVER_18452
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|18452|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|LOGON_INVALID_CONNECT|  
|Message Text|Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.%.\*ls|  
  
## Explanation  
The user attempted to login with credentials that cannot be validated. Possible causes are:  
  
-   The login may be a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login but the server only accepts Windows Authentication.  
  
-   You are trying to connect using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication but the login used does not exist on [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   The login may use Windows Authentication but the login is an unrecognized Windows principal. An unrecognized Windows principal means that the login cannot be verified by Windows. This could be because the Windows login is from an untrusted domain.  
  
Similar problems can cause the less-specific error 18456.  
  
## User Action  
If you are trying to connect using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication, verify that [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is configured in Mixed Authentication Mode.  
  
If you are trying to connect using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication, verify that the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login exists.  
  
If you are trying to connect using Windows Authentication, verify that you are properly logged into the correct domain.  
  
