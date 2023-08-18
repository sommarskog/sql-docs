---
title: "Keep the Locks Configuration Option Default Value"
description: "Keep the Locks Configuration Option Default Value"
author: VanMSFT
ms.author: vanto
ms.date: "03/13/2017"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "Best Practices [Database Engine]"
---
# Keep the Locks Configuration Option Default Value
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This rule checks the value of the locks configuration option. This option determines the maximum number of available locks. This limits how much memory the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] uses for locks. The default setting of 0 enables the [!INCLUDE[ssDE](../../includes/ssde-md.md)] to allocate and deallocate lock structures dynamically based on changing system requirements.  
  
 If locks is nonzero, batch jobs will stop, and an "out of locks" error message will be generated, if the value specified is exceeded.  
  
## Best Practices Recommendations  
 Use the sp_configure system stored procedure to change the value of locks to its default setting by using the following statement:  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## For More Information  
 [Configure the locks Server Configuration Option](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
  
 [Microsoft Knowledge Base article 271509](/troubleshoot/sql/performance/understand-resolve-blocking)  
  
## See Also  
 [Monitor and Enforce Best Practices by Using Policy-Based Management](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
