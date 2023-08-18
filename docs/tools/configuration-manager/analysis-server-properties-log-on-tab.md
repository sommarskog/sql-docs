---
title: "Analysis Server Properties (Log On Tab)"
description: Learn about the Log On tab of the Analysis Server Properties dialog box. See how to use it to specify the SSAS service account and start or stop the service.
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: tools-other
ms.topic: conceptual
monikerRange: ">=sql-server-2016"
---
# Analysis Server Properties (Log On Tab)
[!INCLUDE [SQL Server Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  Use the **Log On** tab of the **Analysis Server Properties** dialog box to specify the account used by the [!INCLUDE[ssAS](../../includes/ssas-md.md)] service, and to start and stop the service.  
  
> [!NOTE]  
>  When changing the **Account Name** used by a service on a clustered instance, the new account must either be a member of the domain group specified during setup for the service being changed, or you must have permission to add members to that group. If you do not have permission to modify group membership, contact the domain administrator.  
  
## Options  
 **Local System account**  
 Specify a local system account, which does not require a password. However, the local system account may restrict the service from interacting with other servers, depending on the privileges granted to the account.  
  
 **This account**  
 Specify a local or domain user account that uses [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Authentication. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recommends using a domain user account with minimal rights for services. For information about selecting an account, search Books Online for the topic Setting Up Windows Service Accounts.  
  
 **Account Name**  
 Specify the local or domain user account name.  
  
 **Password**  
 Type the password of the account.  
  
 **Confirm password**  
 Type the password of the account again.  
  
 **Start**  
 Start the service.  
  
 **Stop**  
 Stop the service.  
  
 **Pause**  
 Pause the service.  
  
 **Resume**  
 Resume a paused service.  
  
  
