---
author: MashaMSFT
ms.author: mathoma
ms.date: 03/29/2023
ms.service: virtual-machines
ms.topic: include
---
- The new [Ebdsv5-series](/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series) provides the highest I/O throughput-to-vCore ratio in Azure along with a memory-to-vCore ratio of 8. This series offers the best price-performance for SQL Server workloads on Azure VMs. Consider this series first for most SQL Server workloads.
- Use VM sizes with 4 or more vCPUs like the [E4ds_v5](/azure/virtual-machines/edv5-edsv5-series#edsv5-series) or higher.
- Use [memory optimized](/azure/virtual-machines/sizes-memory) virtual machine sizes for the best performance of SQL Server workloads.
- The [Edsv5](/azure/virtual-machines/edv5-edsv5-series#edsv5-series) series, the [M-](/azure/virtual-machines/m-series), and the [Mv2-](/azure/virtual-machines/mv2-series) series offer the optimal memory-to-vCore ratio required for OLTP workloads.
- The M series VMs offer the highest memory-to-vCore ratio in Azure. Consider these VMs for mission critical and data warehouse workloads.
- Use Azure Marketplace images to deploy your SQL Server Virtual Machines as the SQL Server settings and storage options are configured for optimal performance.
- Collect the target workload's performance characteristics and use them to determine the appropriate VM size for your business.
- Use the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) and [SKU recommendation](/sql/dma/dma-sku-recommend-sql-db) tools to find the right VM size for your existing SQL Server workload.
- Use [Azure Data Studio](/azure/dms/tutorial-sql-server-to-virtual-machine-online-ads) to migrate to Azure.

