---
title: "Azure CLI example: Failover group - Azure SQL Database elastic pool"
description: Use this Azure CLI example script to create an Azure SQL Database elastic pool, add it to a failover group, and test failover.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: mathoma
ms.date: 01/26/2022
ms.service: sql-database
ms.subservice: high-availability
ms.topic: sample
ms.devlang: azurecli
ms.custom: devx-track-azurecli
---

# Add an Azure SQL Database elastic pool to a failover group using the Azure CLI

[!INCLUDE[appliesto-sqldb](../../includes/appliesto-sqldb.md)]

This Azure CLI script example creates a single database, adds it to an elastic pool, creates a failover group, and tests failover.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/../azure-sql/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Sample script

[!INCLUDE [cli-launch-cloud-shell-sign-in.md](../../includes/cli-launch-cloud-shell-sign-in.md)]

### Run the script

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="FullScript":::

## Clean up resources

[!INCLUDE [cli-clean-up-resources.md](../../includes/cli-clean-up-resources.md)]

```azurecli
az group delete --name $resourceGroup
```

## Sample reference

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Description |
|---|---|
| [az sql elastic-pool](/cli/azure/sql/elastic-pool) | Elastic pool commands. |
| [az sql failover-group](/cli/azure/sql/failover-group) | Failover group commands. |

## Next steps

For more information on Azure CLI, see [Azure CLI documentation](/cli/azure/overview).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../az-cli-script-samples-content-guide.md).
