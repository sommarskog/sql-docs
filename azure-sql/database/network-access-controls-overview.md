---
title: Network Access Controls
titleSuffix: Azure SQL Database & Azure Synapse Analytics
description: Overview of how to manage and control network access for Azure SQL Database and Azure Synapse Analytics.
author: rohitnayakmsft
ms.author: rohitna
ms.reviewer: wiassaf, vanto, mathoma
ms.date: 03/07/2023
ms.service: sql-database
ms.subservice: security
ms.topic: conceptual
ms.custom: sqldbrb=3
---

# Azure SQL Database and Azure Synapse Analytics network access controls

When you create a logical server from the [Azure portal](single-database-create-quickstart.md) for Azure SQL Database and Azure Synapse Analytics, the result is a public endpoint in the format, *yourservername.database.windows.net*.

You can use the following network access controls to selectively allow access to a database via the public endpoint:

- Allow Azure services and resources to access this server: When enabled, other resources within the Azure boundary, for example an Azure Virtual Machine, can access SQL Database
- IP firewall rules: Use this feature to explicitly allow connections from a specific IP address, for example from on-premises machines

You can also allow private access to the database from [virtual networks](/azure/virtual-network/virtual-networks-overview) via:

- Virtual network firewall rules: Use this feature to allow traffic from a specific virtual network within the Azure boundary
- Private Link: Use this feature to create a private endpoint for [logical server in Azure](logical-servers.md) within a specific virtual network

> [!IMPORTANT]
> This article does *not* apply to **SQL Managed Instance**. For more information about the networking configuration, see [connecting to Azure SQL Managed Instance](../managed-instance/connect-application-instance.md) .

See the below video for a high-level explanation of these access controls and what they do:

> [!VIDEO https://learn.microsoft.com/shows/Data-Exposed/Data-Exposed--SQL-Database-Connectivity-Explained/player?WT.mc_id=dataexposed-c9-niner]

## Allow Azure services

By default during creation of a new logical server [from the Azure portal](single-database-create-quickstart.md), **Allow Azure services and resources to access this server** is unchecked and not enabled. This setting appears when connectivity is allowed using public service endpoint.

You can also change this setting via the **Networking** setting after the logical server is created as follows: 
  
![Screenshot of manage server firewall][2]

When **Allow Azure services and resources to access this server** is enabled, your server allows communications from all resources inside the Azure boundary, that may or may not be part of your subscription.

In many cases, enabling the setting is more permissive than what most customers want. You may want to uncheck this setting and replace it with more restrictive IP firewall rules or virtual network firewall rules. 

However, doing so affects the following features that run on virtual machines in Azure that aren't part of your virtual network and hence connect to the database via an Azure IP address:

### Import Export Service

Import Export Service doesn't work when **Allow Azure services and resources to access this server** is not enabled. However you can work around the problem [by manually running SqlPackage from an Azure VM or performing the export](./database-import-export-azure-services-off.md) directly in your code by using the DACFx API.

### Data Sync

To use the Data sync feature with **Allow Azure services and resources to access this server** not enabled, you need to create individual firewall rule entries to [add IP addresses](firewall-create-server-level-portal-quickstart.md) from the **Sql service tag** for the region hosting the **Hub** database. Add these server-level firewall rules to the servers hosting both **Hub** and **Member** databases (which may be in different regions)

Use the following PowerShell script to generate IP addresses corresponding to the SQL service tag for West US region

```powershell
PS C:\>  $serviceTags = Get-AzNetworkServiceTag -Location eastus2
PS C:\>  $sql = $serviceTags.Values | Where-Object { $_.Name -eq "Sql.WestUS" }
PS C:\> $sql.Properties.AddressPrefixes.Count
70
PS C:\> $sql.Properties.AddressPrefixes
13.86.216.0/25
13.86.216.128/26
13.86.216.192/27
13.86.217.0/25
13.86.217.128/26
13.86.217.192/27
```

> [!TIP]
> Get-AzNetworkServiceTag returns the global range for SQL Service Tag despite specifying the Location parameter. Be sure to filter it to the region that hosts the Hub database used by your sync group

Note that the output of the PowerShell script is in Classless Inter-Domain Routing (CIDR) notation. This needs to be converted to a format of Start and End IP address using [Get-IPrangeStartEnd.ps1](https://www.sqltechnet.com/2020/12/powershell-set-azure-sql-firewall-for.html) like this:

```powershell
PS C:\> Get-IPrangeStartEnd -ip 52.229.17.93 -cidr 26
start        end
-----        ---
52.229.17.64 52.229.17.127
```

You can use this additional PowerShell script to convert all the IP addresses from CIDR to Start and End IP address format.

```powershell
PS C:\>foreach( $i in $sql.Properties.AddressPrefixes) {$ip,$cidr= $i.split('/') ; Get-IPrangeStartEnd -ip $ip -cidr $cidr;}
start          end
-----          ---
13.86.216.0    13.86.216.127
13.86.216.128  13.86.216.191
13.86.216.192  13.86.216.223
```

You can now add these as distinct firewall rules and then disable the setting **Allow Azure services and resources to access this server**.

## IP firewall rules

Ip based firewall is a feature of the logical server in Azure that prevents all access to your server until you explicitly [add IP addresses](firewall-create-server-level-portal-quickstart.md) of the client machines.

## Virtual network firewall rules

In addition to IP rules, the server firewall allows you to define *virtual network rules*. To learn more, see [Virtual network service endpoints and rules for Azure SQL Database](vnet-service-endpoint-rule-overview.md) or watch this video:

> [!VIDEO https://learn.microsoft.com/shows/Data-Exposed/Data-Exposed--Demo--Vnet-Firewall-Rules-for-SQL-Database/player?WT.mc_id=dataexposed-c9-niner]

### Azure Networking terminology

Be aware of the following Azure Networking terms as you explore Virtual network firewall rules

**Virtual network:** You can have virtual networks associated with your Azure subscription

**Subnet:** A virtual network contains **subnets**. Any Azure virtual machines (VMs) that you have are assigned to subnets. One subnet can contain multiple VMs or other compute nodes. Compute nodes that are outside of your virtual network can't access your virtual network unless you configure your security to allow access.

**Virtual network service endpoint:** A [Virtual network service endpoint](/azure/virtual-network/virtual-network-service-endpoints-overview) is a subnet whose property values include one or more formal Azure service type names. In this article we're interested in the type name of **Microsoft.Sql**, which refers to the Azure service named SQL Database.

**Virtual network rule:** A virtual network rule for your server is a subnet that is listed in the access control list (ACL) of your server. To be in the ACL for your database in SQL Database, the subnet must contain the **Microsoft.Sql** type name. A virtual network rule tells your server to accept communications from every node that is on the subnet.

## IP vs. Virtual network firewall rules

The Azure SQL Database firewall allows you to specify IP address ranges from which communications are accepted into SQL Database. This approach is fine for stable IP addresses that are outside the Azure private network. However, virtual machines (VMs) within the Azure private network are configured with *dynamic* IP addresses. Dynamic IP addresses can change when your VM is restarted and in turn invalidate the IP-based firewall rule. It would be folly to specify a dynamic IP address in a firewall rule, in a production environment.

You can work around this limitation by obtaining a *static* IP address for your VM. For details, see [Create a virtual machine with a static public IP address using the Azure portal](/azure/virtual-network/ip-services/virtual-network-deploy-static-pip-arm-portal). However, the static IP approach can become difficult to manage, and it's costly when done at scale.

Virtual network rules are easier alternative to establish and to manage access from a specific subnet that contains your VMs.

> [!NOTE]
> You cannot yet have SQL Database on a subnet. If your server was a node on a subnet in your virtual network, all nodes within the virtual network could communicate with your SQL Database. In this case, your VMs could communicate with SQL Database without needing any virtual network rules or IP rules.

## Private Link

Private Link allows you to connect to a server via a **private endpoint**. A private endpoint is a private IP address within a specific [virtual network](/azure/virtual-network/virtual-networks-overview) and Subnet.

## Next steps

- For a quickstart on creating a server-level IP firewall rule, see [Create a database in SQL Database](single-database-create-quickstart.md).

- For a quickstart on creating a server-level virtual network firewall rule, see [Virtual Network service endpoints and rules for Azure SQL Database](vnet-service-endpoint-rule-overview.md).

- For help with connecting to a database in SQL Database from open source or third-party applications, see [Client quickstart code samples to SQL Database](/previous-versions/azure/ee336282(v=azure.100)).

- For information on additional ports that you may need to open, see the **SQL Database: Outside vs inside** section of [Ports beyond 1433 for ADO.NET 4.5 and SQL Database](adonet-v12-develop-direct-route-ports.md)

- For an overview of Azure SQL Database Connectivity, see [Azure SQL Connectivity Architecture](connectivity-architecture.md)

- For an overview of Azure SQL Database security, see [Securing your database](security-overview.md)

<!--Image references-->
[1]: media/quickstart-create-single-database/new-server2.png
[2]: media/quickstart-create-single-database/manage-server-firewall.png
