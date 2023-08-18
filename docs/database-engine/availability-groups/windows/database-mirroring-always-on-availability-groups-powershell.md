---
title: "Powershell: Availability group database mirroring endpoint"
description: "Describes how to create a database mirroring endpoint for an Always On availability group using PowerShell."
author: MashaMSFT
ms.author: mathoma
ms.date: "05/17/2016"
ms.service: sql
ms.subservice: availability-groups
ms.topic: how-to
helpviewer_keywords:
  - "Availability Groups [SQL Server], server instance"
  - "Availability Groups [SQL Server], deploying"
  - "Availability Groups [SQL Server], endpoint"
---
# Create a database mirroring endpoint for an availability group using PowerShell
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  This topic describes how to create a database mirroring endpoint for use by [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] by using PowerShell.  
  

  
##  <a name="Permissions"></a> Permissions  
 Requires CREATE ENDPOINT permission, or membership in the sysadmin fixed server role. For more information, see [GRANT Endpoint Permissions &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  

> [!IMPORTANT]  
>  The RC4 algorithm is deprecated. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] We recommend that you use AES.  
  
##  <a name="PowerShellProcedure"></a> Using PowerShell  
 **To create a database mirroring endpoint**  
  
1.  Change directory (**cd**) to the server instance for which you want to create the database mirroring endpoint.  
  
2.  Use the **New-SqlHadrEndpoint** cmdlet to create the endpoint and then use the **Set-SqlHadrEndpoint** to start the endpoint.  
  
###  <a name="PShellExample"></a> Example (PowerShell)  
 The following PowerShell commands create a database mirroring endpoint on an instance of SQL Server (*Machine*\\*Instance*). The endpoint uses port 5022.  
  
> [!IMPORTANT]  
>  This example works only on a server instance that currently lack a database mirroring endpoint.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> Related Tasks  
 **To Configure a Database Mirroring Endpoint**  
  
-   [Create a Database Mirroring Endpoint for Windows Authentication &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Use Certificates for a Database Mirroring Endpoint &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Allow a Database Mirroring Endpoint to Use Certificates for Outbound Connections &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Allow a Database Mirroring Endpoint to Use Certificates for Inbound Connections &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Specify a Server Network Address &#40;Database Mirroring&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Specify the Endpoint URL When Adding or Modifying an Availability Replica &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **To View Information About the Database Mirroring Endpoint**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## See Also  
 [Create an Availability Group &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Overview of Always On Availability Groups &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
