---
title: Fail over a database with the link via T-SQL & PowerShell or Azure CLI scripts
titleSuffix: Azure SQL Managed Instance
description: Learn how to use Transact-SQL (T-SQL) and PowerShell or Azure CLI scripts to fail over a database from SQL Server to SQL Managed Instance by using the Managed Instance link.
author: sasapopo
ms.author: sasapopo
ms.reviewer: mathoma, danil
ms.date: 04/26/2023
ms.service: sql-managed-instance
ms.subservice: data-movement
ms.custom: devx-track-azurepowershell, devx-track-azurecli
ms.topic: how-to
---

# Failover (migrate) a database with a link via T-SQL and PowerShell or Azure CLI scripts - Azure SQL Managed Instance 

[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

This article teaches you how to use Transact-SQL (T-SQL) and Azure PowerShell or Azure CLI scripts and a [Managed Instance link](managed-instance-link-feature-overview.md) to fail over (migrate) your database from SQL Server to SQL Managed Instance.

Database failover from SQL Server 2019 and earlier to SQL Managed Instance breaks the link between the two databases. Failover stops replication and leaves both databases in an independent state, ready for individual read/write workloads.  

Failing over from SQL Server 2022 does not break the link, and fail back to SQL Server 2022 is supported - this is currently in preview. 

> [!TIP]
> - To simplify using T-SQL scripts with the correct parameters for your environment, we strongly recommend using the Managed Instance link wizard in [SQL Server Management Studio (SSMS)](managed-instance-link-use-ssms-to-failover-database.md#fail-over-a-database) to generate the script to fail over a database. On the **Summary** page of the **Failover database to Managed Instance** window, select **Script** instead of **Finish**. 

## Prerequisites 

To replicate your databases to SQL Managed Instance, you need the following prerequisites: 

- An active Azure subscription. If you don't have one, [create a free account](https://azure.microsoft.com/free/).
- [Supported version of SQL Server](managed-instance-link-feature-overview.md#prerequisites) with required service update installed.
- Azure SQL Managed Instance. [Get started](instance-create-quickstart.md) if you don't have it. 
- PowerShell module [Az.SQL 3.9.0](https://www.powershellgallery.com/packages/Az.Sql), or higher
- A properly [prepared environment](managed-instance-link-preparation.md).

## Stop workload

To start migrating your database to SQL Managed Instance, first stop any application workloads on SQL Server during your maintenance hours. This enables database replication to catch up on SQL Managed Instance so you can migrate to Azure while without data loss. While the primary database is a part of an Always On availability group, you can't set it to read-only mode. You need to ensure that your applications aren't committing transactions to SQL Server prior to the failover.

## Switch the replication mode

Replication between SQL Server and SQL Managed Instance is asynchronous by default. Before you migrate your database to Azure, switch the link to synchronous mode. Synchronous replication across large network distances might slow down transactions on the primary SQL Server instance.

Switching from async to sync mode requires a replication mode change on both SQL Managed Instance and SQL Server.

### Switch replication mode (SQL Managed Instance)

Use either Azure Powershell or the Azure CLI to switch the replication mode on SQL Managed Instance. 

First, ensure that you're logged in to Azure and that you've selected the subscription where your managed instance is hosted. Selecting the proper subscription is especially important if you have more than one Azure subscription on your account. 

Replace `<SubscriptionID>` with your Azure subscription ID. 


#### [PowerShell](#tab/powershell)

```powershell-interactive
# Run in Azure Cloud Shell (select PowerShell console)

# Enter your Azure subscription ID
$SubscriptionID = "<SubscriptionID>"

# Login to Azure and select subscription ID
if ((Get-AzContext ) -eq $null)
{
    echo "Logging to Azure subscription"
    Login-AzAccount
}
Select-AzSubscription -SubscriptionName $SubscriptionID
```

#### [Azure CLI](#tab/azure-cli)


```azurecli-interactive
# Run in Azure Cloud Shell (select Bash console) 
# Enter your Azure subscription ID 
SubscriptionID="<SubscriptionID>" 

# Login to Azure Bash and select subscription ID 
echo "Logging to Azure subscription " $SubscriptionID 
az account set --subscription $SubscriptionID 
```

---

Ensure that you know the name of the link you would like to fail over. Use the below script to list all active links on managed instance. 

Replace `<ManagedInstanceName>` with the short name of your managed instance. 
 

#### [PowerShell](#tab/powershell)

```powershell-interactive
# Run in Azure Cloud Shell (select PowerShell console)
# =============================================================================
# POWERSHELL SCRIPT TO LIST ALL LINKS ON MANAGED INSTANCE
# ===== Enter user variables here ====

# Enter your managed instance name – for example, "sqlmi1"
$ManagedInstanceName = "<ManagedInstanceName>"

# ==== Do not customize the following cmdlet ====

# Find out the resource group name
$ResourceGroup = (Get-AzSqlInstance -InstanceName $ManagedInstanceName).ResourceGroupName

# List all links on the specified managed instance
Get-AzSqlInstanceLink -ResourceGroupName $ResourceGroup -InstanceName $ManagedInstanceName 
```

#### [Azure CLI](#tab/azure-cli)


```azurecli-interactive
# Run in Azure Cloud Shell (select Bash console) 
# ============================================================================= 
# CLI SCRIPT TO LIST ALL LINKS ON MANAGED INSTANCE 
# ===== Enter user variables here ====  

# Enter your managed instance name – for example, "sqlmi1" 
ManagedInstanceName="<ManagedInstanceName>" 

# Enter Resource Group for your managed instance 
ResourceGroup="<ResourceGroup>" 

# ==== Do not customize the following cmdlet ==== 
az sql mi link list --resource-group $ResourceGroup --instance-name $ManagedInstanceName
```

---

From the output of the previous script, record the `Name` property of the link you'd like to fail over.

Then, switch the replication mode from async to sync on managed instance for the identified link by running the following script. Replace:
- `<ManagedInstanceName>` with the short name of your managed instance. 
- `<DAGName>` with the name of the link you found out on the previous step (the `Name` property from the previous step).

#### [PowerShell](#tab/powershell)

```powershell-interactive
# Run in Azure Cloud Shell (select PowerShell console)
# =============================================================================
# POWERSHELL SCRIPT TO SWITCH LINK REPLICATION MODE (ASYNC\SYNC)
# ===== Enter user variables here ====

# Enter the link name 
$LinkName = "<DAGName>"  

# Enter your managed instance name – for example, "sqlmi1" 
$ManagedInstanceName = "<ManagedInstanceName>" 

# ==== Do not customize the following cmdlet ====

# Find out the resource group name
$ResourceGroup = (Get-AzSqlInstance -InstanceName $ManagedInstanceName).ResourceGroupName

# Update replication mode of the specified link
Update-AzSqlInstanceLink -ResourceGroupName $ResourceGroup -InstanceName $ManagedInstanceName |
-Name $LinkName -ReplicationMode "Sync"
```

#### [Azure CLI](#tab/azure-cli)


```azurecli-interactive
# Run in Azure Cloud Shell (select Bash console) 
# ============================================================================= 
# CLI SCRIPT TO SWITCH LINK REPLICATION MODE (ASYNC\SYNC) 
# ===== Enter user variables here ====  

# Enter the link name 
LinkName="<DAGName>"  

# Enter the availability group name that was created on SQL Server 
AGName="<AGName>" 

# Enter your managed instance name – for example, "sqlmi1" 
ManagedInstanceName="<ManagedInstanceName>" 

# Enter Resource Group for your managed instance 
ResourceGroup="<ResourceGroup>" 

# ==== Do not customize the following cmdlet ==== 
# Update replication mode of the specified link 

az sql mi link update --resource-group $ResourceGroup --instance-name $ManagedInstanceName
--distributed-availability-group-name $LinkName --primary-ag $AGName
--secondary-ag=$ManagedInstanceName --replication-mode "Sync" 
```

---

The previous command indicates success by displaying a summary of the operation, with the property `ReplicationMode` shown as `Sync`.

If you need to revert the operation, execute the previous script to switch the replication mode but replace the `Sync` string in the `-ReplicationMode` to `Async`.

### Switch replication mode (SQL Server)

Use the following T-SQL script on SQL Server to change the replication mode of the distributed availability group on SQL Server from async to sync. Replace:
- `<DAGName>` with the name of the distributed availability group (used to create the link).
- `<AGName>` with the name of the availability group created on SQL Server (used to create the link). 
- `<ManagedInstanceName>` with the name of your managed instance.

```sql
-- Run on SQL Server
-- Sets the distributed availability group to a synchronous commit.
-- ManagedInstanceName example: 'sqlmi1'
USE master
GO
ALTER AVAILABILITY GROUP [<DAGName>] 
MODIFY 
AVAILABILITY GROUP ON
    '<AGName>' WITH
    (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    '<ManagedInstanceName>' WITH
    (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
```

To confirm that you've changed the link's replication mode successfully, use the following dynamic management view. Results indicate the `SYNCHRONOUS_COMIT` state.

```sql
-- Run on SQL Server
-- Verifies the state of the distributed availability group
SELECT
    ag.name, ag.is_distributed, ar.replica_server_name,
    ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc,
    ars.operational_state_desc, ars.synchronization_health_desc
FROM
    sys.availability_groups ag
    join sys.availability_replicas ar
    on ag.group_id=ar.group_id
    left join sys.dm_hadr_availability_replica_states ars
    on ars.replica_id=ar.replica_id
WHERE
    ag.is_distributed=1
```

Now that you've switched both SQL Managed Instance and SQL Server to sync mode, replication between the two instances is synchronous. If you need to reverse this state, follow the same steps and set the async state for both SQL Server and SQL Managed Instance.

## Check LSN values on both SQL Server and SQL Managed Instance

To complete the migration, confirm that replication has finished. For this, ensure the log sequence numbers (LSNs) in the log records for both SQL Server and SQL Managed Instance are the same. 

Initially, it's expected that the SQL Server LSN will be higher than the SQL Managed Instance LSN. Network latency might cause SQL Managed Instance to lag somewhat behind the primary SQL Server instance. Because the workload has been stopped on SQL Server, you should expect the LSNs to match and stop changing after some time. 

Use the following T-SQL query on SQL Server to read the LSN of the last recorded transaction log. Replace:
- `<DatabaseName>` with your database name and look for the last hardened LSN number.

```sql
-- Run on SQL Server
-- Obtain the last hardened LSN for the database on SQL Server.
SELECT
    ag.name AS [Replication group],
    db.name AS [Database name], 
    drs.database_id AS [Database ID], 
    drs.group_id, 
    drs.replica_id, 
    drs.synchronization_state_desc AS [Sync state], 
    drs.end_of_log_lsn AS [End of log LSN],
    drs.last_hardened_lsn AS [Last hardened LSN] 
FROM
    sys.dm_hadr_database_replica_states drs
    inner join sys.databases db on db.database_id = drs.database_id
    inner join sys.availability_groups ag on drs.group_id = ag.group_id
WHERE
    ag.is_distributed = 1 and db.name = '<DatabaseName>'
```

Use the following T-SQL query on SQL Managed Instance to read the last hardened LSN for your database. Replace `<DatabaseName>` with your database name.

This query will work on a General Purpose managed instance. For a Business Critical managed instance, you need to uncomment `and drs.is_primary_replica = 1` at the end of the script. On Business Critical, this filter ensures that only primary replica details are read.

```sql
-- Run on a managed instance
-- Obtain the LSN for the database on SQL Managed Instance.
SELECT
    db.name AS [Database name],
    drs.database_id AS [Database ID], 
    drs.group_id, 
    drs.replica_id, 
    drs.synchronization_state_desc AS [Sync state],
    drs.end_of_log_lsn AS [End of log LSN],
    drs.last_hardened_lsn AS [Last hardened LSN]
FROM
    sys.dm_hadr_database_replica_states drs
    inner join sys.databases db on db.database_id = drs.database_id
WHERE
    db.name = '<DatabaseName>'
    -- for Business Critical, add the following as well
    -- AND drs.is_primary_replica = 1
```

Alternatively, you could also use Azure PowerShell command [Get-AzSqlInstanceLink](/powershell/module/az.sql/get-azsqlinstancelink), or the Azure CLI command [az sql mi link show](/cli/azure/sql/mi/link#az-sql-mi-link-show), to fetch the `LastHardenedLsn` property for your link on SQL Managed Instance which provides the same information as the above T-SQL query.


> [!IMPORTANT]
> Verify once again that your workload is stopped on SQL Server. Check that LSNs on both SQL Server and SQL Managed Instance match, and that they **remain matched** and unchanged for some time. Stable LSNs on both instances indicate that the tail log has been replicated to SQL Managed Instance and the workload is effectively stopped.

## Start database failover and migration to Azure

Run the below script in Azure Cloud Shell to finalize your migration to Azure. The script breaks the link and ends replication to SQL Managed Instance for SQL Server 2019 and earlier. The replicated database becomes read/write on the managed instance. Replace:
- `<ManagedInstanceName>` with the name of your managed instance. 
- `<DAGName>` with the name of the link you're failing over (output of the property `Name` from `Get-AzSqlInstanceLink` command executed earlier above).

#### [PowerShell](#tab/powershell)

```powershell-interactive
# Run in Azure Cloud Shell (select PowerShell console) 
# =============================================================================
# POWERSHELL SCRIPT TO FAILOVER AND MIGRATE DATABASE TO AZURE
# ===== Enter user variables here ====

# Enter your managed instance name – for example, "sqlmi1"
$ManagedInstanceName = "<ManagedInstanceName>"
$LinkName = "<DAGName>"

# ==== Do not customize the following cmdlet ====

# Find out the resource group name
$ResourceGroup = (Get-AzSqlInstance -InstanceName $ManagedInstanceName).ResourceGroupName

# Failover the specified link
Remove-AzSqlInstanceLink -ResourceGroupName $ResourceGroup |
-InstanceName $ManagedInstanceName -Name $LinkName -Force
```

#### [Azure CLI](#tab/azure-cli)

```azurecli-interactive
# Run in Azure Cloud Shell (select Bash console) 
# ============================================================================= 
# CLI SCRIPT TO FAILOVER AND MIGRATE DATABASE TO AZURE 
# ===== Enter user variables here ==== 

# Enter the link name 
LinkName="<DAGName>" 

# Enter your managed instance name – for example, "sqlmi1" 
ManagedInstanceName="<ManagedInstanceName>" 
 
# Enter Resource Group for your managed instance
ResourceGroup="<ResourceGroup>" 

# ==== Do not customize the following cmdlet ====  

# Failover the specified link 
az sql mi link delete --resource-group $ResourceGroup --instance-name $ManagedInstanceName
--distributed-availability-group-name $LinkName --yes 
```

---

When failover succeeds, the link is dropped and no longer exists. The source SQL Server database and the target SQL Managed Instance database can both execute a read/write workload. They're completely independent. Repoint your application connection string to managed instance to complete the migration process.

> [!IMPORTANT]
> After a successful failover, manually repoint your application(s) connection string to the managed instance FQDN to complete the migration process and continue running in Azure.

## Clean up availability groups

After you break the link and migrate a database to Azure SQL Managed Instance, consider cleaning up the availability group and distributed availability group resources from SQL Server if they're no longer necessary. 

In the following code, replace:

- `<DAGName>` with the name of the distributed availability group on SQL Server (used to create the link). 
- `<AGName>` with the name of the availability group on SQL Server (used to create the link).

``` sql
-- Run on SQL Server
USE MASTER
GO
DROP AVAILABILITY GROUP <DAGName>
GO
DROP AVAILABILITY GROUP <AGName>
GO
```

With this step, you've finished the migration of the database from SQL Server to SQL Managed Instance.

## Next steps

For more information on the link feature, see the following resources:

- [Managed Instance link – connecting SQL Server to Azure reimagined](https://aka.ms/mi-link-techblog)
- [Prepare your environment for Managed Instance link](./managed-instance-link-preparation.md)
- [Use a Managed Instance link with scripts to replicate a database](./managed-instance-link-use-scripts-to-replicate-database.md)
- [Use a Managed Instance link via SSMS to replicate a database](./managed-instance-link-use-ssms-to-replicate-database.md)
- [Use a Managed Instance link via SSMS to migrate a database](./managed-instance-link-use-ssms-to-failover-database.md)
