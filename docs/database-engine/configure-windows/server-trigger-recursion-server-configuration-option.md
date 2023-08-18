---
title: "server trigger recursion (server configuration option)"
description: "Learn how the server trigger recursion option affects recursion in SQL Server server-level triggers. See how to turn direct and indirect recursion on and off."
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/02/2017"
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "recursive triggers [SQL Server]"
  - "triggers [SQL Server], recursive"
  - "server trigger recursion option"
---
# server trigger recursion (server configuration option)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use the **server trigger recursion** option to specify whether to allow server-level triggers to fire recursively. When this option is set to 1 (ON), server-level triggers will be allowed to fire recursively. When set to 0 (OFF), server-level triggers cannot be fired recursively. Only direct recursion is prevented when the server trigger recursion option is set to 0 (OFF). (To disable indirect recursion, set the **nested triggers** option to 0.) The default value for this option is 1 (ON). The setting takes effect immediately (without a server restart).  
  
 For more information, see [Create Nested Triggers](../../relational-databases/triggers/create-nested-triggers.md).  
  
## See Also  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Server Configuration Options &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
