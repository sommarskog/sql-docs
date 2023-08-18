---
title: "Symmetric Keys on User Databases"
description: "Symmetric Keys on User Databases"
author: VanMSFT
ms.author: vanto
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "Best Practices [Database Engine]"
---
# Symmetric Keys on User Databases
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This rule checks whether keys that have a length of less than 128 bytes do not use the RC2 or RC4 encryption algorithm.  
  
## Best Practices Recommendations  
 Use AES 128 bit or larger to create symmetric keys for data encryption. If AES is not supported by your operating system, use 3DES.  
  
## For More Information  
 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## See Also  
 [Monitor and Enforce Best Practices by Using Policy-Based Management](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
