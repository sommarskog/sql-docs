---
title: Change the license model for a SQL VM in Azure
description: Learn how to switch licensing for a SQL Server VM in Azure from pay-as-you-go to bring-your-own-license by using the Azure Hybrid Benefit.
author: bluefooted
ms.author: pamela
ms.reviewer: mathoma, randolphwest
ms.date: 03/15/2023
ms.service: virtual-machines-sql
ms.subservice: management
ms.topic: how-to
tags: azure-resource-manager
---
# Change the license model for a SQL virtual machine in Azure

[!INCLUDE[appliesto-sqlvm](../../includes/appliesto-sqlvm.md)]

This article describes how to change the license model for a SQL Server virtual machine (VM) in Azure by using the [SQL IaaS Agent Extension](./sql-server-iaas-agent-extension-automate-management.md).

## Overview

There are three license models for an Azure VM that's hosting SQL Server: pay-as-you-go, Azure Hybrid Benefit (AHB), and High Availability/Disaster Recovery(HA/DR). You can modify the license model of your SQL Server VM by using the Azure portal, the Azure CLI, or PowerShell.

- The **pay-as-you-go** model means that the per-second cost of running the Azure VM includes the cost of the SQL Server license.
- [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit/) allows you to use your own SQL Server license with a VM that's running SQL Server.
- The **HA/DR** license type is used for the [free HA/DR replica](business-continuity-high-availability-disaster-recovery-hadr-overview.md#free-dr-replica-in-azure) in Azure.

Azure Hybrid Benefit allows the use of SQL Server licenses with Software Assurance ("Qualified License") on Azure virtual machines. With Azure Hybrid Benefit, customers aren't charged for the use of a SQL Server license on a VM. But they must still pay for the cost of the underlying cloud compute (that is, the base rate), storage, and backups. They must also pay for I/O associated with their use of the services (as applicable).

To estimate your cost savings with the Azure Hybrid benefit, use the [Azure Hybrid Benefit Savings Calculator](https://azure.microsoft.com/pricing/hybrid-benefit/#calculator). To estimate the cost of Pay as you Go licensing, review the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).

According to the Microsoft [Product Terms](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftAzureServices/EAEAS): "Customers must indicate that they are using Azure SQL Database (Managed Instance, Elastic Pool, and Single Database), Azure Data Factory, SQL Server Integration Services, or SQL Server Virtual Machines under Azure Hybrid Benefit for SQL Server when configuring workloads on Azure."

To indicate the use of Azure Hybrid Benefit for SQL Server on Azure VM and be compliant, you have three options:

- Provision a virtual machine by using a bring-your-own-license SQL Server image from Azure Marketplace. This option is available only for customers who have an Enterprise Agreement.
- Provision a virtual machine by using a pay-as-you-go SQL Server image from Azure Marketplace and activate the Azure Hybrid Benefit.
- Self-install SQL Server on Azure VM, manually [register with the SQL IaaS Agent Extension](sql-agent-extension-manually-register-single-vm.md), and activate Azure Hybrid Benefit.

The license type of SQL Server can be configured when the VM is provisioned, or anytime afterward. Switching between license models incurs no downtime, does not restart the VM or the SQL Server service, doesn't add any additional costs, and is effective immediately. In fact, activating Azure Hybrid Benefit *reduces* cost.

## Prerequisites

Changing the licensing model of your SQL Server VM has the following requirements:

- An [Azure subscription](https://azure.microsoft.com/free/).
- A [SQL Server VM](./create-sql-vm-portal.md) registered with the [SQL IaaS Agent Extension](./sql-server-iaas-agent-extension-automate-management.md).
- [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default) is a requirement to utilize the [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit/) license type, but pay-as-you-go customers can use the **HA/DR** license type if the VM is being used as a passive replica in a high availability/disaster recovery configuration.

## Change license model

# [Azure portal](#tab/azure-portal)

You can modify the license model directly from the portal:

1. Open the [Azure portal](https://portal.azure.com) and open the [SQL virtual machines resource](manage-sql-vm-portal.md#access-the-resource) for your SQL Server VM.
1. Select **Configure** under **Settings**.
1. Select the **Azure Hybrid Benefit** option, and select the check box to confirm that you have a SQL Server license with Software Assurance.
1. Select **Apply** at the bottom of the **Configure** page.

:::image type="content" source="./media/licensing-model-azure-hybrid-benefit-ahb-change/ahb-in-portal.png" alt-text="Screenshot showing the Azure Hybrid Benefit in the portal.":::

# [Azure CLI](#tab/azure-cli)

You can use the Azure CLI to change your license model.

Specify the following values for **license-type**:
- `AHUB` for the Azure Hybrid Benefit
- `PAYG` for pay as you go
- `DR` to activate the free HA/DR replica

```azurecli-interactive
# example: az sql vm update -n AHBTest -g AHBTest --license-type AHUB

az sql vm update -n <VMName> -g <ResourceGroupName> --license-type <license-type>
```

# [PowerShell](#tab/azure-powershell)

You can use PowerShell to change your license model.

Specify the following values for **license-type**:
- `AHUB` for the Azure Hybrid Benefit
- `PAYG` for pay as you go
- `DR` to activate the free HA/DR replica

```powershell-interactive
Update-AzSqlVM -ResourceGroupName <resource_group_name> -Name <VM_name> -LicenseType <license-type>
```

---

## Remarks

- Azure Cloud Solution Provider (CSP) customers can use the Azure Hybrid Benefit by first deploying a pay-as-you-go VM and then converting it to bring-your-own-license, if they have active Software Assurance.
- If you drop your SQL virtual machines resource, you will go back to the hard-coded license setting of the image.
- The ability to change the license model is a feature of the SQL IaaS Agent Extension. Deploying an Azure Marketplace image through the Azure portal automatically registers a SQL Server VM with the extension. But customers who are self-installing SQL Server will need to manually [register their SQL Server VM](sql-agent-extension-manually-register-single-vm.md).
- Adding a SQL Server VM to an availability set requires re-creating the VM. As such, any VMs added to an availability set will go back to the default pay-as-you-go license type. Azure Hybrid Benefit will need to be enabled again.

## Limitations

Changing the license model is:

- Only supported for the Standard and Enterprise editions of SQL Server. License changes for Express, Web, and Developer are not supported.
- Only supported for virtual machines deployed through the Azure Resource Manager model. Virtual machines deployed through the classic model are not supported.

Additionally, changing the license model to **Azure Hybrid Benefit** requires [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-overview).

> [!NOTE]  
> Only SQL Server core-based licensing with Software Assurance or subscription licenses are eligible for Azure Hybrid Benefit. If you are using Server + CAL licensing for SQL Server and you have Software Assurance, you can use bring-your-own-license to an Azure SQL Server virtual machine image to leverage license mobility for these servers, but you cannot leverage the other features of Azure Hybrid Benefit.

## Remove a SQL Server instance and its associated licensing and billing costs

**Before you begin**

To avoid being charged for your SQL Server instance, see [Pricing guidance for SQL Server on Azure VMs](/azure/azure-sql/virtual-machines/windows/pricing-guidance).

To remove a SQL Server instance and associated billing from a Pay-As-You-Go SQL Server VM, or if you are being charged for a SQL instance after uninstalling it:

1. Back up your data.
1. If necessary, uninstall SQL Server, including the SQL IaaS Agent extension.
1. Download the free [SQL Server Express](https://www.microsoft.com/sql-server/sql-server-downloads) edition.
1. Install the [SQL IaaS Agent extension](/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-single-vm).
1. To stop billing, [change edition in the portal](/azure/azure-sql/virtual-machines/windows/change-sql-server-edition#change-edition-property-for-billing) to Express edition.

**Optional**

To disable the SQL Server Express edition service, disable service startup.

**Common issues and questions related to licensing**

Review the [Licensing FAQ](/azure/azure-sql/virtual-machines/windows/frequently-asked-questions-faq#licensing) to see the most common questions.

## Known errors

Review the commonly known errors and their resolutions.

**The Resource 'Microsoft.SqlVirtualMachine/SqlVirtualMachines/\<resource-group>' under resource group '\<resource-group>' was not found.**

This error occurs when you try to change the license model on a SQL Server VM that has not been registered with the SQL IaaS Agent extension:

`The Resource 'Microsoft.SqlVirtualMachine/SqlVirtualMachines/\<resource-group>' under resource group '\<resource-group>' was not found. The property 'sqlServerLicenseType' cannot be found on this object. Verify that the property exists and can be set.`

You'll need to [register your SQL Server VM with the SQL IaaS Agent extension](sql-agent-extension-manually-register-single-vm.md).

**Change licensing to AHB, BYOL, HADR or PAYG**

Make sure your [subscription is registered with resource provider (RP)](/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-single-vm#register-subscription-with-rp).

The SQL IaaS Agent extension is required to change the license. Make sure you [remove and reinstall the SQL IaaS Agent extension](/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-single-vm#register-in-full-mode) if it's in a failed state.

**SQL Server edition, version, or licensing on Azure Portal does not reflect correctly after edition or version upgrade**

Make sure your [subscription is registered with resource provider (RP)](/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-single-vm#register-subscription-with-rp).

The SQL IaaS Agent extension is required to change the license. Make sure you [repair the extension](/azure/azure-sql/virtual-machines/windows/sql-agent-extension-manually-register-single-vm?#repair-extension) if it's in a failed state.

## Next steps

For more information, see the following articles:

- [Overview of SQL Server on a Windows VM](sql-server-on-azure-vm-iaas-what-is-overview.md)
- [FAQ for SQL Server on a Windows VM](frequently-asked-questions-faq.yml)
- [Pricing guidance for SQL Server on a Windows VM](pricing-guidance.md)
- [What's new for SQL Server on Azure VMs](doc-changes-updates-release-notes-whats-new.md)
- [Overview of SQL IaaS Agent Extension](./sql-server-iaas-agent-extension-automate-management.md)
