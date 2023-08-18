---
title: Connectivity architecture
titleSuffix: Azure SQL Managed Instance
description: Learn about Azure SQL Managed Instance communication and connectivity architecture and how the components direct traffic for a managed instance.
author: zoran-rilak-msft
ms.author: zoranrilak
ms.reviewer: mathoma, bonova
ms.date: 08/02/2023
ms.service: sql-managed-instance
ms.subservice: service-overview
ms.topic: conceptual
ms.custom: fasttrack-edit, build-2023, build-2023-dataai
---

# Connectivity architecture for Azure SQL Managed Instance

[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

This article describes the connectivity architecture in Azure SQL Managed Instance and how components direct communication traffic for a managed instance.  

## Overview

In SQL Managed Instance, an instance is placed inside the Azure virtual network and inside the subnet that's dedicated to managed instances. The deployment provides:

- A secure virtual network-local (VNet-local) IP address.
- The ability to connect an on-premises network to SQL Managed Instance.
- The ability to connect SQL Managed Instance to a linked server or to another on-premises data store.
- The ability to connect SQL Managed Instance to Azure resources.

> [!NOTE]
> The November 2022 feature wave introduced changes to the default connectivity structure of SQL Managed Instance. This article provides information about the current architecture and the architecture of instances that haven't yet enrolled in the feature wave. For more information, see [November 2022 feature wave](doc-changes-updates-release-notes-whats-new.md#november-2022-feature-wave).

## November 2022 feature wave

The November 2022 feature wave introduced the following changes to the SQL Managed Instance connectivity architecture:

- Removed the management endpoint.
- Simplified mandatory network security group rules (removed one mandatory rule).
- Revised mandatory network security group rules so they no longer include outbound to AzureCloud on port 443.
- Simplified the route table (reduced mandatory routes from 13 to 5).

## High-level connectivity architecture

## [Current architecture](#tab/current)

At a high level, SQL Managed Instance is made of up service components hosted on a dedicated set of isolated virtual machines that are joined to a virtual cluster. Some service components are deployed inside the customer's virtual network subnet while other services operate within a secure network environment that Microsoft manages.

:::image type="content" source="media/connectivity-architecture-overview/2-connectivity-architecture-diagram-sql-managed-instance.png" border="false" alt-text="Diagram that shows the high-level connectivity architecture for Azure SQL Managed Instance after November 2022.":::

A virtual cluster can host multiple managed instances. The cluster automatically expands or contracts as needed to accommodate new and removed instances.

Customer applications can connect to SQL Managed Instance and can query and update databases inside the virtual network, peered virtual network, or network connected by VPN or Azure ExpressRoute.

The following diagram shows entities that connect to SQL Managed Instance. It also shows the resources that need to communicate with a managed instance. The communication process at the bottom of the diagram represents customer applications and tools that connect to SQL Managed Instance as data sources.  

:::image type="content" source="media/connectivity-architecture-overview/1-connectivity-architecture-diagram-entities.png" border="false" alt-text="Diagram that shows entities in the connectivity architecture for Azure SQL Managed Instance after November 2022.":::

SQL Managed Instance is a single-tenant, platform as a service offering that operates in two planes: a data plane and a control plane.

The *data plane* is deployed inside the customer's subnet for compatibility, connectivity, and network isolation. Data plane depends on Azure services like Azure Storage, Azure Active Directory (Azure AD) for authentication, and telemetry collection services. You'll see traffic that originates in subnets that contain SQL Managed Instance going to those services.

The *control plane* carries the deployment, management, and core service maintenance functions via automated agents. These agents have exclusive access to the compute resources that operate the service. You can't use `ssh` or Remote Desktop Protocol to access those hosts. All control plane communications are encrypted and signed by using certificates. To check the trustworthiness of communicating parties, SQL Managed Instance constantly verifies these certificates by using certificate revocation lists.

## [Architecture prior to November 2022](#tab/before-feature-wave)

At a high level, SQL Managed Instance is a set of service components that are hosted on a dedicated set of isolated virtual machines that are joined to a virtual cluster. Some service components are deployed inside the customer's virtual network subnet. Other services operate in a secure network environment that Microsoft manages.

:::image type="content" source="media/connectivity-architecture-overview/02-connectivity-architecture-sql-managed-instance.png" border="false" alt-text="Diagram that shows the high-level connectivity architecture for Azure SQL Managed Instance before November 2022.":::

A virtual cluster can host multiple managed instances. The cluster automatically expands or contracts as needed to accommodate new and removed instances.

Customer applications can connect to SQL Managed Instance and can query and update databases inside the virtual network, peered virtual network, or network connected by VPN or Azure ExpressRoute.

The following diagram shows entities that connect to SQL Managed Instance. It also shows the resources that need to communicate with a managed instance. The communication process at the bottom of the diagram represents customer applications and tools that connect to SQL Managed Instance as data sources.  

:::image type="content" source="media/connectivity-architecture-overview/01-connectivity-architecture-entities.png" border="false" alt-text="Diagram that shows entities in the connectivity architecture for SQL Managed Instance before November 2022.":::

SQL Managed Instance is a single-tenant, platform as a service (PaaS) offering. Its compute and networking elements are deployed inside the customer's subnet. SQL Managed Instance typically is accessed via its [VNet-local endpoint](connectivity-architecture-overview.md#vnet-local-endpoint). SQL Managed Instance depends on Azure services like Azure Storage, Azure Active Directory (Azure AD), Azure Key Vault, Azure Event Hubs, and telemetry collection services. Traffic that originates in subnets that contain SQL Managed Instance might go to those services.

Deployment, management, and core service maintenance operations are carried out via automated agents. These agents have exclusive access to the compute resources that operate the service. You can't use `ssh` or Remote Desktop Protocol to access those hosts. All internal communications are encrypted and signed by using certificates. To check the trustworthiness of communicating parties, SQL Managed Instance constantly verifies these certificates by using certificate revocation lists.

### Management endpoint

To facilitate communication between the control plane and the components deployed inside the customer's subnet, managed instances not yet enrolled in the November 2022 Feature Wave employ a management endpoint. This means that elements of the virtual network's infrastructure can harm management traffic by making the instance fail and become unavailable. Management and deployment services connect to SQL Managed Instance's management endpoint which is mapped to an external load balancer. Traffic is routed to the nodes only if it's received on a predefined set of ports that only the management components of SQL Managed Instance use. A built-in firewall on the nodes is set up to allow traffic only from Microsoft IP ranges. Certificates mutually authenticate all communication between management components and the management plane.

> [!NOTE]
> Traffic that goes to Azure services that are inside the SQL Managed Instance region is optimized. Because the traffic is optimized, traffic isn't sent by Network Address Translation (NAT) to the public IP address for the management endpoint. If you need to use IP-based firewall rules, most commonly for storage, the service must be in a different region than SQL Managed Instance.

The Azure SQL Managed Instance [mandatory inbound security rules](connectivity-architecture-overview.md#mandatory-security-rules-with-service-aided-subnet-configuration) require management ports 9000, 9003, 1438, 1440, and 1452 to be open from *any source* on the network security group (NSG) that protects SQL Managed Instance. Although these ports are open at the network security group level, they're protected at the network level by the built-in firewall.

The management endpoint is protected by a built-in firewall on the network level. On the application level, it's protected by mutual certificate verification. When connections start inside SQL Managed Instance, like in backups and audit logs, traffic appears to start from the management endpoint's public IP address.

---

## Communication overview

Applications can connect to SQL Managed Instance via three types of endpoints. These endpoints serve different scenarios and exhibit distinct network properties and behaviors.

- [VNet-local endpoint](#vnet-local-endpoint)
- [Public endpoint](#public-endpoint)
- [Private endpoints](#private-endpoints)

:::image type="content" source="media/connectivity-architecture-overview/4-connectivity-architecture-endpoints.png" border="false" alt-text="Diagram that shows the scope of visibility for VNet-local, public, and private endpoints to an Azure SQL Managed Instance.":::

### VNet-local endpoint

The VNet-local endpoint is the default means to connect to SQL Managed Instance. The VNet-local endpoint is a domain name in the form of `<mi_name>.<dns_zone>.database.windows.net` that resolves to an IP address from the subnet's address pool; hence **VNet-local**, or an endpoint that is local to the virtual network. The VNet-local endpoint can be used to connect to a SQL Managed Instance in all standard connectivity scenarios.

VNet-local endpoints support the [redirect connection type](connection-types-overview.md).

When connecting to the VNet-local endpoint, always use its domain name as the underlying IP address may occasionally change.

### Public endpoint

The public endpoint is an optional domain name in the form of `<mi_name>.public.<dns_zone>.database.windows.net` that resolves to a public IP address reachable from the Internet. Public endpoint allows TDS traffic only to reach SQL Managed Instance on port 3342 and cannot be used for integration scenarios, such as failover groups, Managed Instance Link, and similar.

When connecting to the VNet-local endpoint, always use its domain name as the underlying IP address may occasionally change.

Public endpoint always operates in [proxy connection type](connection-types-overview.md).

Learn how to set up a public endpoint in [Configure public endpoint for Azure SQL Managed Instance](public-endpoint-configure.md).

### Private endpoints

A private endpoint is an optional fixed IP address in another virtual network that conducts traffic to your SQL managed instance. One Azure SQL Managed Instance can have multiple private endpoints in multiple virtual networks. Private endpoints allow TDS traffic only to reach SQL Managed Instance on port 1433 and cannot be used for integration scenarios, such as failover groups, Managed Instance link, and other similar technologies.

When connecting to a private endpoint, always use the domain name since connecting to Azure SQL Managed Instance via its IP address is not supported yet.

Private endpoints always operate in [proxy connection type](connection-types-overview.md).

Learn more about private endpoints and how to configure them in [Azure Private Link for Azure SQL Managed Instance](private-endpoint-overview.md).



## Virtual cluster connectivity architecture

This section provides a closer look at the virtual cluster connectivity architecture of SQL Managed Instance. The following diagram shows the conceptual layout of the virtual cluster:

## [Current architecture](#tab/current)

:::image type="content" source="media/connectivity-architecture-overview/3-connectivity-architecture-diagram-virtual-cluster.png" border="false" alt-text="Diagram that shows the virtual cluster connectivity architecture for Azure SQL Managed Instance after November 2022.":::

## [Architecture prior to November 2022](#tab/before-feature-wave)

:::image type="content" source="media/connectivity-architecture-overview/03-connectivity-architecture-virtual-cluster.png" border="false" alt-text="Diagram that shows the virtual cluster connectivity architecture for Azure SQL Managed Instance before November 2022.":::

---

The domain name of the VNet-local endpoint resolves to the private IP address of an internal load balancer. Although this domain name is registered in a public Domain Name System (DNS) zone and is publicly resolvable, its IP address belongs to the subnet's address range and can only be reached from inside its virtual network by default.

The load balancer directs traffic to a SQL Managed Instance gateway. Because multiple managed instances can run inside the same cluster, the gateway uses the SQL Managed Instance host name as seen in the connection string to redirect traffic to the correct SQL engine service.

The value for `zone-id` is automatically generated when you create the cluster. If a newly created cluster hosts a secondary managed instance, it shares its zone ID with the primary cluster.

## Service-aided subnet configuration

To improve service security, manageability, and availability, SQL Managed Instance applies a network intent policy on some elements of the Azure virtual network infrastructure. The policy configures the subnet, the associated network security group, and the route table to ensure that the minimum requirements for SQL Managed Instance are met. This platform mechanism transparently communicates networking requirements to users. The policy's main goal is to prevent network misconfiguration and to ensure normal SQL Managed Instance operations and service-level agreement commitment. When you delete a managed instance, the network intent policy is also removed.

A service-aided subnet configuration builds on top of the virtual network [subnet delegation](/azure/virtual-network/subnet-delegation-overview) feature to provide automatic network configuration management and to enable service endpoints.

You can use service endpoints to configure virtual network firewall rules on storage accounts that keep backups and audit logs. Even with service endpoints enabled, customers are encouraged to use [Azure Private Link](/azure/private-link/private-link-overview) to access their storage accounts. Private Link provides more isolation than service endpoints.

> [!IMPORTANT]
> Due to control plane configuration specificities, a service-aided subnet configuration doesn't enable service endpoints in national clouds.

### Network requirements

The subnet in which SQL Managed Instance is deployed must have the following characteristics:

- **Dedicated subnet**: The subnet SQL Managed Instance uses can be delegated only to the SQL Managed Instance service. The subnet can't be a gateway subnet, and you can deploy only SQL Managed Instance resources in the subnet.
- **Subnet delegation**: The SQL Managed Instance subnet must be delegated to the `Microsoft.Sql/managedInstances` resource provider.
- **Network security group**: A network security group must be associated with the SQL Managed Instance subnet. You can use a network security group to control access to the SQL Managed Instance data endpoint by filtering traffic on port 1433 and ports 11000-11999 when SQL Managed Instance is configured for redirect connections. The service automatically provisions [rules](#mandatory-security-rules-with-service-aided-subnet-configuration) and keeps them current as required to allow uninterrupted flow of management traffic.
- **Route table**: A route table must be associated with the SQL Managed Instance subnet. You can add entries to the route table to route traffic that has on-premises private IP address ranges as a destination through the virtual network gateway or virtual network appliance. The service automatically provisions [entries](#mandatory-routes-with-service-aided-subnet-configuration) and keeps them current as required to allow uninterrupted flow of management traffic.
- **Sufficient IP addresses**: The SQL Managed Instance subnet must have at least 32 IP addresses. For more information, see [Determine the size of the subnet for SQL Managed Instance](vnet-subnet-determine-size.md). You can deploy managed instances in the [existing network](vnet-existing-add-subnet.md) after you configure it to satisfy the [networking requirements for SQL Managed Instance](#network-requirements). Otherwise, create a [new network and subnet](virtual-network-subnet-create-arm-template.md).
- **Allowed by Azure policies**: If you use [Azure Policy](/azure/governance/policy/overview) to prevent resource creation or modification in a scope that includes a SQL Managed Instance subnet or virtual network, your policies must not prevent SQL Managed Instance from managing its internal resources. The following resources need to be excluded from policy deny effects for normal operation:
  - Resources of type `Microsoft.Network/serviceEndpointPolicies`, when resource name begins with `\_e41f87a2\_`
  - All resources of type `Microsoft.Network/networkIntentPolicies`
  - All resources of type `Microsoft.Network/virtualNetworks/subnets/contextualServiceEndpointPolicies`
- **Locks on virtual network**: [Locks](/azure/azure-resource-manager/management/lock-resources) on the dedicated subnet's virtual network, its parent resource group, or subscription, might occasionally interfere with SQL Managed Instance management and maintenance operations. Take special care when you use resource locks.
- **Replication traffic**: Replication traffic for auto-failover groups between two managed instances should be direct and not routed through a hub network.
- **Custom DNS server:** If the virtual network is configured to use a custom DNS server, the DNS server must be able to resolve public DNS records. Using features like Azure AD authentication might require resolving more fully qualified domain names (FQDNs). For more information, see [Resolving private DNS names in Azure SQL Managed Instance](resolve-private-domain-names.md).


### Mandatory security rules with service-aided subnet configuration

## [Current architecture](#tab/current)

To ensure inbound management traffic flow, the rules described in the following table are required. The rules are enforced by the network intent policy and don't need to be deployed by the customer. For more information about the connectivity architecture and management traffic, see [High-level connectivity architecture](#high-level-connectivity-architecture).

|Name          |Port                        |Protocol|Source           |Destination|Action|
|--------------|----------------------------|--------|-----------------|-----------|------|
|healthprobe-in|Any                         |Any     |AzureLoadBalancer|_subnet_   |Allow |
|internal-in   |Any                         |Any     |_subnet_         |_subnet_   |Allow |

To ensure outbound management traffic flow, the rules described in the following table are required. For more information about the connectivity architecture and management traffic, see [High-level connectivity architecture](#high-level-connectivity-architecture).

|Name               |Port          |Protocol|Source           |Destination               |Action|
|-------------------|--------------|--------|-----------------|--------------------------|------|
|AAD-out            |443           |TCP     |_subnet_         |AzureActiveDirectory      |Allow |
|OneDsCollector-out |443           |TCP     |_subnet_         |OneDsCollector            |Allow |
|internal-out       |Any           |Any     |_subnet_         |_subnet_                  |Allow |
|StorageP-out       |443           |Any     |_subnet_         |Storage._primaryRegion_   |Allow |
|StorageS-out       |443           |Any     |_subnet_         |Storage._secondaryRegion_ |Allow |

## [Architecture prior to November 2022](#tab/before-feature-wave)

To ensure inbound management traffic flow, the rules described in the following table are required:

| Name       |Port                        |Protocol|Source           |Destination|Action|
|------------|----------------------------|--------|-----------------|-----------|------|
|management  |9000, 9003, 1438, 1440, 1452|TCP     |SqlManagement    |MI SUBNET  |Allow |
|            |9000, 9003                  |TCP     |CorpnetSaw       |MI SUBNET  |Allow |
|            |9000, 9003                  |TCP     |CorpnetPublic    |MI SUBNET  |Allow |
|mi_subnet   |Any                         |Any     |MI SUBNET        |MI SUBNET  |Allow |
|health_probe|Any                         |Any     |AzureLoadBalancer|MI SUBNET  |Allow |

To ensure outbound management traffic flow, the rules described in the following table are required:

| Name       |Port          |Protocol|Source           |Destination|Action|
|------------|--------------|--------|-----------------|-----------|------|
|management  |443, 12000    |TCP     |MI SUBNET        |AzureCloud |Allow |
|mi_subnet   |Any           |Any     |MI SUBNET        |MI SUBNET  |Allow |

---

### Mandatory routes with service-aided subnet configuration

## [Current architecture](#tab/current)

The routes that are described in the following table are necessary to ensure that management traffic is routed directly to a destination. The routes are enforced by the network intent policy and don't need to be deployed by the customer. For more information about connectivity architecture and management traffic, see [High-level connectivity architecture](#high-level-connectivity-architecture).

|Name                     |Address prefix           |Next hop            |
|-------------------------|-------------------------|--------------------|
|AzureActiveDirectory     |AzureActiveDirectory     |Internet<sup>*</sup>|
|OneDsCollector           |OneDsCollector           |Internet<sup>*</sup>|
|Storage._primaryRegion_  |Storage._primaryRegion_  |Internet<sup>*</sup>|
|Storage._secondaryRegion_|Storage._secondaryRegion_|Internet<sup>*</sup>|
|subnet-to-vnetlocal      |_subnet_                 |Virtual network     |

> [!NOTE]
> <sup>*</sup> The **Internet** value in the **Next hop** column instructs the gateway to route the traffic outside the virtual network. However, if the destination address is for an Azure service, Azure routes the traffic directly to the service over the Azure network instead of outside the Azure cloud. Traffic between Azure services doesn't traverse the internet, regardless of which Azure region the virtual network exists in or which Azure region an instance of the Azure service is deployed to. For more information, see [Azure virtual network traffic routing](/azure/virtual-network/virtual-networks-udr-overview).

You also can add entries to the route table to route traffic that has on-premises private IP ranges as a destination through the virtual network gateway or virtual network appliance.

## [Architecture prior to November 2022](#tab/before-feature-wave)

The routes that are described in the following table are necessary to ensure that management traffic is routed directly to a destination:

|Name|Address prefix|Next hop <sup>2</sup>|
|----|--------------|-------|
|subnet-to-vnetlocal|MI SUBNET <sup>1</sup>|Virtual network|
|mi-azurecloud-REGION-internet|AzureCloud.REGION|Internet|
|mi-azurecloud-REGION_PAIR-internet|AzureCloud.REGION_PAIR|Internet|
|mi-azuremonitor-internet|AzureMonitor|Internet|
|mi-corpnetpublic-internet|CorpNetPublic|Internet|
|mi-corpnetsaw-internet|CorpNetSaw|Internet|
|mi-eventhub-REGION-internet|EventHub.REGION|Internet|
|mi-eventhub-REGION_PAIR-internet|EventHub.REGION_PAIR|Internet|
|mi-sqlmanagement-internet|SqlManagement|Internet|
|mi-storage-internet|Storage|Internet|
|mi-storage-REGION-internet|Storage.REGION|Internet|
|mi-storage-REGION_PAIR-internet|Storage.REGION_PAIR|Internet|
|mi-azureactivedirectory-internet|AzureActiveDirectory|Internet|

---

### Networking constraints

**TLS 1.2 is enforced on outbound connections**: Beginning in January 2020, Microsoft enforces TLS 1.2 for intra-service traffic in all Azure services. For SQL Managed Instance, this resulted in TLS 1.2 being enforced on outbound connections that are used for replication and on linked server connections to SQL Server. If you use a version of SQL Server that's earlier than 2016 with SQL Managed Instance, make sure that you apply [TLS 1.2-specific updates](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

The following virtual network features are currently *not supported* with SQL Managed Instance:

- **Microsoft peering**: Enabling [Microsoft peering](/azure/expressroute/expressroute-faqs#microsoft-peering) on ExpressRoute circuits that are peered directly or transitively with a virtual network in which SQL Managed Instance resides affects traffic flow between SQL Managed Instance components inside the virtual network and services it depends on. Availability issues result. SQL Managed Instance deployments to a virtual network that already has Microsoft peering enabled are expected to fail.
- **Global virtual network peering**: [Virtual network peering](/azure/virtual-network/virtual-network-peering-overview) connectivity across Azure regions doesn't work for instances of SQL Managed Instance that are placed in subnets that were created before September 9, 2020.
- **AzurePlatformDNS**: Using the AzurePlatformDNS [service tag](/azure/virtual-network/service-tags-overview) to block platform DNS resolution would render SQL Managed Instance unavailable. Although SQL Managed Instance supports customer-defined DNS for DNS resolution inside the engine, there's a dependency on platform DNS for platform operations.
- **NAT gateway**: Using [Azure Virtual Network NAT](/azure/virtual-network/nat-gateway/nat-overview) to control outbound connectivity with a specific public IP address renders SQL Managed Instance unavailable. The SQL Managed Instance service is currently limited to use the basic load balancer, which doesn't provide coexistence of inbound and outbound flows with Azure Virtual Network NAT.
- **IPv6 for Azure Virtual Network**: Deploying SQL Managed Instance to [dual stack IPv4/IPv6 virtual networks](/azure/virtual-network/ip-services/ipv6-overview) is expected to fail. Associating a network security group or a route table with user-defined routes (UDRs) that contains IPv6 address prefixes to a SQL Managed Instance subnet renders SQL Managed Instance unavailable. Also, adding IPv6 address prefixes to a network security group or UDR that's already associated with a managed instance subnet renders SQL Managed Instance unavailable. SQL Managed Instance deployments to a subnet with a network security group and UDR that already have IPv6 prefixes are expected to fail.
- **Azure DNS private zones with a name reserved for Microsoft services**: The following domain names are reserved names: `windows.net`, `database.windows.net`, `core.windows.net`, `blob.core.windows.net`, `table.core.windows.net`, `management.core.windows.net`, `monitoring.core.windows.net`, `queue.core.windows.net`, `graph.windows.net`, `login.microsoftonline.com`, `login.windows.net`, `servicebus.windows.net`, and `vault.azure.net`. Deploying SQL Managed Instance to a virtual network that has an associated [Azure DNS private zone](/azure/dns/private-dns-privatednszone) that uses a name reserved for Microsoft services fails. Associating an Azure DNS private zone that uses a reserved name with a virtual network that contains a managed instance renders SQL Managed Instance unavailable. For information about Private Link configuration, see [Azure Private Endpoint DNS configuration](/azure/private-link/private-endpoint-dns).

## Next steps

- For an overview, see [What is Azure SQL Managed Instance?](sql-managed-instance-paas-overview.md).
- Learn how to [set up a new Azure virtual network](virtual-network-subnet-create-arm-template.md) or an [existing Azure virtual network](vnet-existing-add-subnet.md) where you can deploy SQL Managed Instance.
- [Calculate the size of the subnet](vnet-subnet-determine-size.md) where you want to deploy SQL Managed Instance.
- Learn how to create a managed instance:
  - From the [Azure portal](instance-create-quickstart.md).
  - By using [PowerShell](scripts/create-configure-managed-instance-powershell.md).
  - By using [an Azure Resource Manager template](https://azure.microsoft.com/resources/templates/sqlmi-new-vnet/).
  - By using [an Azure Resource Manager template with a jumpbox and SQL Server Management Studio](https://azure.microsoft.com/resources/templates/sqlmi-new-vnet-w-jumpbox/).
