---
title: "Azure CLI example: Backup a database in Azure SQL Database"
description: Use this Azure CLI example script to backup an Azure SQL single database to an Azure storage container
author: SudhirRaparla
ms.author: nvraparl
ms.reviewer: mathoma
ms.date: 01/26/2022
ms.service: sql-database
ms.subservice: backup-restore
ms.topic: sample
ms.custom: devx-track-azurecli
ms.devlang: azurecli
---

# Backup an Azure SQL single database to an Azure storage container using the Azure CLI

[!INCLUDE[appliesto-sqldb](../../includes/appliesto-sqldb.md)]

This Azure CLI example backs up a database in SQL Database to an Azure storage container.  

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](~/../azure-sql/reusable-content/azure-cli/azure-cli-prepare-your-environment.md)]

## Sample script

[!INCLUDE [cli-launch-cloud-shell-sign-in.md](../../includes/cli-launch-cloud-shell-sign-in.md)]

### Run the script

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/backup-database/backup-database.sh" id="FullScript":::

## Clean up resources

[!INCLUDE [cli-clean-up-resources.md](../../includes/cli-clean-up-resources.md)]

```azurecli
az group delete --name $resourceGroup
```

## Sample reference

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az sql server](/cli/azure/sql/server) | Server commands. |
| [az sql db](/cli/azure/sql/db) | Database commands. |

## Next steps

For more information on Azure CLI, see [Azure CLI documentation](/cli/azure).

Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../az-cli-script-samples-content-guide.md).
