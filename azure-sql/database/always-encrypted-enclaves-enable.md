---
title: "Enable Always Encrypted with secure enclaves in Azure SQL Database"
description: Learn how to enable secure enclaves in Azure SQL Database and elastic pools by selecting Intel SGX-enabled hardware or virtualization-based security (VBS)
author: Pietervanhove
ms.author: pivanho
ms.reviewer: vanto
ms.date: 07/19/2023
ms.service: sql-database
ms.subservice: security
ms.custom: devx-track-azurecli, devx-track-azurepowershell
ms.topic: conceptual
---
# Enable Always Encrypted with secure enclaves in Azure SQL Database

[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

In Azure SQL Database, [Always Encrypted with secure enclaves](/sql/relational-databases/security/encryption/always-encrypted-enclaves) can use either [Intel Software Guard Extensions (Intel SGX) enclaves](https://www.intel.com/content/www/us/en/architecture-and-technology/software-guard-extensions.html) or [Virtualization-based Security (VBS) enclaves](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/). For more information, see [Plan for secure enclaves in Azure SQL Database](always-encrypted-enclaves-plan.md).

## [Intel SGX enclaves](#tab/IntelSGXenclaves)

For Intel SGX to be available, the database must use the [vCore model](service-tiers-vcore.md) and [DC-series](service-tiers-sql-database-vcore.md#dc-series) hardware.

Configuring the DC-series hardware to enable Intel SGX enclaves is the responsibility of the Azure SQL Database administrator. For more information, see [Roles and responsibilities when configuring Intel SGX enclaves and attestation](always-encrypted-enclaves-plan.md#roles-and-responsibilities-when-configuring-intel-sgx-enclaves-and-attestation).

> [!NOTE]
> Intel SGX is not available in hardware configurations other than DC-series. For example, Intel SGX is not available for standard-series (Gen5) hardware, and it is not available for databases using the [DTU model](service-tiers-dtu.md).

> [!IMPORTANT]
> Before you configure the DC-series hardware for your database, check the regional availability of DC-series and make sure you understand its performance limitations. For more information, see [DC-series](service-tiers-sql-database-vcore.md#dc-series).

For detailed instructions on how to configure a new or existing database to use a specific hardware configuration, see [Hardware configuration](service-tiers-sql-database-vcore.md#hardware-configuration).

## Next steps

- [Configure Azure Attestation for your Azure SQL database server](always-encrypted-enclaves-configure-attestation.md)

## [VBS enclaves](#tab/VBSenclaves)

> [!IMPORTANT]
> The VBS enclaves feature in Azure SQL Database is currently in preview. The [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, in preview, or otherwise not yet released into general availability.

By default, a new database is created without VBS enclaves. To enable a VBS enclave in your database or elastic pool, you need to set the **preferredEnclaveType** [database property](/azure/templates/microsoft.sql/2022-05-01-preview/servers/databases?pivots=deployment-language-bicep#databaseproperties) to **VBS**, which activates the VBS enclave for the database or the elastic pool. You can set **preferredEnclaveType** when you create a new database or elastic pool or by updating an existing database or elastic pool. Any database you add to an elastic pool will inherit the enclave property from it, like the database SLO. Hence, if you add a database without VBS enclaves enabled to an elastic pool with VBS enabled, this new database becomes part of elastic pool and VBS enclaves will be enabled on this database. Adding a database with VBS enclaves enabled to an elastic pool without VBS enclaves is not supported. 

You can set the **preferredEnclaveType** using Azure PowerShell or the Azure CLI.

## Enabling VBS enclaves with Azure PowerShell

Create a new database with a VBS enclave with the [New-AzSqlDatabase](/powershell/module/az.sql/New-AzSqlDatabase) cmdlet. The following example creates a serverless database with a VBS enclave.

```azurepowershell-interactive
New-AzSqlDatabase  -ResourceGroupName "ResourceGroup01" `
    -ServerName "Server01" `
    -DatabaseName "Database01" `
    -Edition GeneralPurpose `
    -ComputeModel Serverless `
    -ComputeGeneration Gen5 `
    -VCore 2 `
    -MinimumCapacity 2 `
    -PreferredEnclaveType VBS
```

Create a new elastic pool with a VBS enclave with the [New-AzSqlElasticPool](/powershell/module/az.sql/New-AzSqlElasticPool) cmdlet. The following example creates an elastic pool with a VBS enclave.

```azurepowershell-interactive
New-AzSqlElasticPool ` 
    -ComputeGeneration Gen5 `
    -Edition 'GeneralPurpose' `
    -ElasticPoolName $ElasticPoolName `
    -ResourceGroupName $resourceGroupName `
    -ServerName $serverName `
    -VCore 2 `
    -PreferredEnclaveType 'VBS'
```

To enable a VBS enclave for an existing database, use the [Set-AzSqlDatabase](/powershell/module/az.sql/Set-AzSqlDatabase) cmdlet. Here's an example:

```azurepowershell-interactive
Set-AzSqlDatabase -ResourceGroupName "ResourceGroup01" `
    -DatabaseName "Database01" `
    -ServerName "Server01" `
    -PreferredEnclaveType VBS
```

To enable a VBS enclave for an existing elastic pool, use the [Set-AzSqlElasticPool](/powershell/module/az.sql/Set-AzSqlElasticPool) cmdlet. Here's an example:

```azurepowershell-interactive
Set-AzSqlElasticPool `
    -ResourceGroupName $resourceGroupName `
    -ServerName $serverName `
    -ElasticPoolName $ElasticPoolName `
    -PreferredEnclaveType 'VBS' 
```

## Enabling VBS enclaves with Azure CLI

Create a new database with a VBS enclave with the [az sql db create](/cli/azure/sql/db) cmdlet. The following example creates a serverless database with a VBS enclave.

```azurecli-interactive
az sql db create -g ResourceGroup01 `
    -s Server01 `
    -n Database01 `
    -e GeneralPurpose `
    --compute-model Serverless `
    -f Gen5 `
    -c 2 `
    --min-capacity 2 `
    --preferred-enclave-type VBS 
```

Create a new elastic pool with a VBS enclave with the [az sql elastic-pool create](/cli/azure/sql/elastic-pool) cmdlet. The following example creates a serverless database with a VBS enclave.

```azurecli-interactive
az sql elastic-pool create -g ResourceGroup01 `
    -s Server01 `
    -n ElasticPool01 `
    -e GeneralPurpose `
    -f Gen5 `
    -c 2 `
    --preferred-enclave-type VBS
```

To enable a VBS enclave for an existing database, use the [az sql db update](/cli/azure/sql/db) cmdlet. Here's an example:

```azurecli-interactive
az sql db update -g ResourceGroup01 `
    -s Server01 `
    -n Database01 `
    --preferred-enclave-type VBS
```
To enable a VBS enclave for an existing elastic pool, use the [az sql elastic-pool update](/cli/azure/sql/elastic-pool) cmdlet. Here's an example:

```azurecli-interactive
az sql elastic-pool update -g ResourceGroup01 `
    -s Server01 `
    -n ElasticPool01 `
    --preferred-enclave-type VBS
```

---

## See also

- [Getting started using Always Encrypted with secure enclaves](always-encrypted-enclaves-getting-started.md)
