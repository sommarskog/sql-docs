---
title: "MSSQLSERVER_26014"
description: "MSSQLSERVER_26014"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "26014 (Database Engine error)"
---
# MSSQLSERVER_26014
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|26014|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|SNI_SSL_USER_CERT_FAILURE|  
|Message Text|Unable to load user-specified certificate [Cert Hash(sha1) "%hs"]. The server will not accept a connection. You should verify that the certificate is correctly installed. See "Configuring Certificate for Use by SSL" in Books Online.|  
  
## Explanation  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempted to load the certificate named in the message but the operation failed. This problem must be resolved before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can use this certificate.  
  
Possible causes of the error include:  
  
-   The certificate could have been moved or deleted.  
  
-   If the login used by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] has changed, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] may not have permission to access the certificate.  
  
-   The certificate may have expired.  
  
## User Action  
Make sure the certificate named in the message exists on the system, is accessible, and it is valid for use.  
  
