---
title: Load sample data
titleSuffix: SQL Server Big Data Clusters
description: This tutorial demonstrates how to load sample data into a SQL Server big data cluster. The sample data includes relational data in the SQL Server master instance. It also includes HDFS data in the storage pool. This data supports other tutorials in this section.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: hudequei
ms.date: 08/21/2019
ms.service: sql
ms.subservice: big-data-cluster
ms.topic: tutorial
---

# Tutorial: Load sample data into a SQL Server big data cluster

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE[big-data-clusters-banner-retirement](../includes/bdc-banner-retirement.md)]

This tutorial explains how to use a script to load sample data into a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Many of the other tutorials in the documentation use this sample data.

> [!TIP]
> You can find additional samples for [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] in the [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster) GitHub repository. They are located in the **sql-server-samples/samples/features/sql-big-data-cluster/** path.

## Prerequisites

- [A deployed big data cluster](deployment-guidance.md)
- [Big data tools](deploy-big-data-tools.md)
   - **azdata**
   - **kubectl**
   - **sqlcmd**
   - **curl**
 
## <a id="sampledata"></a> Load sample data

The following steps use a bootstrap script to download a SQL Server database backup and load the data into your big data cluster. For ease of use, these steps have been broken out into [Windows](#windows) and [Linux](#linux) sections. If you want to use basic username/password as authentication mechanism then set AZDATA_USERNAME and AZDATA_PASSWORD environment variables before executing the script. Otherwise the script will use integrated authentication to connect to SQL Server Master instance and Knox gateway. Also, DNS name should be specified for the endpoints in order to use integrated authentication.

## <a id="windows"></a> Windows

The following steps describe how to use a Windows client to load the sample data into your big data cluster.

1. Open a new Windows command prompt.

   > [!IMPORTANT]
   > Do not use Windows PowerShell for these steps. In PowerShell, the script will fail as it will use the PowerShell version of **curl**.

1. Use **curl** to download the bootstrap script for the sample data.

   ```cmd
   curl -o bootstrap-sample-db.cmd "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd"
   ```

1. Download the **bootstrap-sample-db.sql** Transact-SQL script. This script is called by the bootstrap script.

   ```cmd
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. The bootstrap script requires the following positional parameters for your big data cluster:

   | Parameter | Description |
   |---|---|
   | <CLUSTER_NAMESPACE> | The name you gave your big data cluster. |
   | <SQL_MASTER_ENDPOINT> | The DNS name or IP address of your master instance. |
   | <KNOX_ENDPOINT> | The DNS name or IP address of the HDFS/Spark Gateway. |
   
   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) to find the IP addresses for the SQL Server master instance and Knox. Run `kubectl get svc -n <your-big-data-cluster-name>` and look at the EXTERNAL-IP addresses for the master instance (**master-svc-external**) and Knox (**gateway-svc-external**). The default name of a cluster is **mssql-cluster**.

1. Run the bootstrap script.

   ```cmd
   .\bootstrap-sample-db.cmd <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## <a id="linux"></a> Linux

The following steps describe how to use a Linux client to load the sample data into your big data cluster.

1. Download the bootstrap script, and assign executable permissions to it.

   ```bash
   curl -o bootstrap-sample-db.sh "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh"
   chmod +x bootstrap-sample-db.sh
   ```

1. Download the **bootstrap-sample-db.sql** Transact-SQL script. This script is called by the bootstrap script.

   ```bash
   curl -o bootstrap-sample-db.sql "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql"
   ```

1. The bootstrap script requires the following positional parameters for your big data cluster:

   | Parameter | Description |
   |---|---|
   | <CLUSTER_NAMESPACE> | The name you gave your big data cluster. |
   | <SQL_MASTER_ENDPOINT> | The DNS name or IP address of your master instance. |
   | <KNOX_ENDPOINT> | The DNS name or IP address of the HDFS/Spark Gateway. |

   > [!TIP]
   > Use [kubectl](cluster-troubleshooting-commands.md) to find the IP addresses for the SQL Server master instance and Knox. Run `kubectl get svc -n <your-big-data-cluster-name>` and look at the EXTERNAL-IP addresses for the master instance (**master-svc-external**) and Knox (**gateway-svc-external**). The default name of a cluster is **mssql-cluster**.

1. Run the bootstrap script.

   ```bash
   ./bootstrap-sample-db.sh <CLUSTER_NAMESPACE> <SQL_MASTER_ENDPOINT> <KNOX_ENDPOINT>
   ```

## Next steps

After the bootstrap script runs, your big data cluster has the sample databases and HDFS data. The following tutorials use the sample data to demonstrate big data cluster capabilities:

Data Virtualization:

- [Tutorial: Query HDFS in a SQL Server big data cluster](tutorial-query-hdfs-storage-pool.md)
- [Tutorial: Query Oracle from a SQL Server big data cluster](tutorial-query-oracle.md)

Data ingestion:

- [Tutorial: Ingest data into a SQL Server data pool with Transact-SQL](tutorial-data-pool-ingest-sql.md)
- [Tutorial: Ingest data into a SQL Server data pool with Spark jobs](tutorial-data-pool-ingest-spark.md)

Notebooks:

- [Tutorial: Run a sample notebook on a SQL Server 2019 big data cluster](notebooks-tutorial-spark.md)
