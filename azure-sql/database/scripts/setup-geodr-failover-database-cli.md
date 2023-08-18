---
title: "Azure CLI example: Active geo-replication-single Azure SQL Database"
description: Use this Azure CLI example script to set up active geo-replication for a single database in Azure SQL Database and fail it over.
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

# Configure active geo-replication for a single database in Azure SQL Database using the Azure CLI

[!INCLUDE[appliesto-sqldb](../../includes/appliesto-sqldb.md)]

This Azure CLI script example configures active geo-replication for a single database and fails it over to a secondary replica of the database.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/../azure-sql/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Sample script

[!INCLUDE [cli-launch-cloud-shell-sign-in.md](../../includes/cli-launch-cloud-shell-sign-in.md)]

### Run the script

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/setup-geodr-and-failover/setup-geodr-and-failover-single-database.sh" id="FullScript":::

## Clean up resources

[!INCLUDE [cli-clean-up-resources.md](../../includes/cli-clean-up-resources.md)]

```azurecli
az group delete --name $resourceGroup
```

## Sample reference

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Description |
|---|---|
| [az sql db replica](/cli/azure/sql/db/replica) | Database replica commands. |

## Next steps

For more information on Azure CLI, see [Azure CLI documentation](/cli/azure).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../az-cli-script-samples-content-guide.md).
