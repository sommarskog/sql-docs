---
title: Resolve capacity errors with Azure SQL resources
description: Learn how to resolve possible capacity errors when attempting to deploy or scale Azure SQL Database or Azure SQL Managed Instance resources.
author: sachinpMSFT
ms.author: sachinp
ms.reviewer: mathoma
ms.date: 09/03/2021
ms.service: sql-db-mi
ms.subservice: deployment-configuration
ms.topic: how-to
ms.custom: references_regions
---

# Resolve capacity errors with Azure SQL Database or Azure SQL Managed Instance
[!INCLUDE[appliesto-sqldb-sqlmi](includes/appliesto-sqldb-sqlmi.md)]

In this article, learn how to resolve capacity errors when deploying Azure SQL Database or Azure SQL Managed Instance resources. 

## Exceeded quota 

If you encounter any of the following errors when attempting to deploy your Azure SQL resource, please [request to increase your quota](database/quota-increase-request.md): 

- `Server quota limit has been reached for this location. Please select a different location with lower server count.`
- `Could not perform the operation because server would exceed the allowed Database Throughput Unit quota of xx.`
- During a scale operation, you may see the following error:    
  `Could not perform the operation because server would exceed the allowed Database Throughput Unit quota of xx. `. 

## Subscription access

Your subscription may not have access to create a server in the selected region if your subscription has not been registered with the SQL resource provider (RP).  

If you see the following errors, please [register your subscription with the SQL RP](#register-with-sql-rp):
- `Your subscription does not have access to create a server in the selected region.`
- `Provisioning is restricted in this region. Please choose a different region. For exceptions to this rule please open a support request with issue type of 'Service and subscription limits' `
- `Location 'region name' is not accepting creation of new Windows Azure SQL Database servers for the subscription 'subscription id' at this time`


## Enable region 

Your subscription may not have access to create a server in the selected region if that region has not been enabled. To resolve this, file a [support request to enable a specific region](database/quota-increase-request.md#region) for your subscription. 

If you see the following errors, file a support ticket to enable a specific region: 
- `Your subscription does not have access to create a server in the selected region.`
- `Provisioning is restricted in this region. Please choose a different region. For exceptions to this rule please open a support request with issue type of 'Service and subscription limits' `
- `Location 'region name' is not accepting creation of new Windows Azure SQL Database servers for the subscription 'subscription id' at this time`



## Register with SQL RP

To deploy Azure SQL resources, register your subscription with the SQL resource provider (RP). 

You can register your subscription using the Azure portal, [the Azure CLI](/cli/azure/install-azure-cli), or [Azure PowerShell](/powershell/azure/install-az-ps). 

# [Azure portal](#tab/portal)

To register your subscription in the Azure portal, follow these steps: 

1. Open the Azure portal and go to **All Services**.
1. Go to **Subscriptions** and select the subscription of interest.
1. On the **Subscriptions** page, select **Resource providers** under **Settings**.
1. Enter **sql** in the filter to bring up the SQL-related extensions.
1. Select **Register**, **Re-register**, or **Unregister** for the  **Microsoft.Sql** provider, depending on your desired action.

   ![Modify the provider](./media/capacity-errors-troubleshoot/register-with-sql-rp.png)

# [Azure CLI](#tab/bash)

To register your subscription using [the Azure CLI](/cli/azure/install-azure-cli), run this cmdlet:

```azurecli-interactive
# Register the SQL resource provider to your subscription 
az provider register --namespace Microsoft.Sql 
```

# [Azure PowerShell](#tab/powershell)

To register your subscription using [Azure PowerShell](/powershell/azure/install-az-ps), run this cmdlet: 

```powershell-interactive
# Register the SQL resource provider to your subscription
Register-AzResourceProvider -ProviderNamespace Microsoft.Sql

```

---

## Additional provisioning issues

If you're still experiencing provisioning issues, please open a **Region** access request under the support topic of SQL Database and specify the DTU or vCores you want to consume on Azure SQL Database or Azure SQL Managed Instance. 

## Azure Program regions 

Azure Program offerings (Azure Pass, Imagine, Azure for Students, MPN, BizSpark, BizSpark Plus, Microsoft for Startups / Sponsorship Offers, Visual Studio Subscriptions / MSDN) have access to a limited set of regions. 

If your subscription is part of an Azure Program offering, and you would like to request access to any of the following regions, please consider using an alternate region instead: 

_Australia Central, Australia Central 2, Australia SouthEast, Brazil SouthEast, Canada East, China East, China North, China North 2, France South, Germany North, Japan West, JIO India Central, JIO India West, Korea South, Norway West, South Africa West, South India, Switzerland West, UAE Central , UK West, US DoD Central, US DoD East, US Gov Arizona, US Gov Texas, West Central US, West India._ 

## Next steps

After you submit your request, it will be reviewed. You will be contacted with an answer based on the information you provided in the form.

For more information about other Azure limits, see [Azure subscription and service limits, quotas, and constraints](/azure/azure-resource-manager/management/azure-subscription-service-limits).
