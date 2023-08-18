---
title: Monitoring and performance tuning
description: An overview of monitoring and performance tuning capabilities and methodology in Azure SQL Database and Azure SQL Managed Instance.
author: dimitri-furman
ms.author: dfurman
ms.reviewer: wiassaf, mathoma, urmilano
ms.date: 11/30/2022
ms.service: sql-db-mi
ms.subservice: performance
ms.topic: conceptual
ms.custom: sqldbrb=2
monikerRange: "= azuresql || = azuresql-db || = azuresql-mi"
---
# Monitoring and performance tuning in Azure SQL Database and Azure SQL Managed Instance
[!INCLUDE[appliesto-sqldb-sqlmi](../includes/appliesto-sqldb-sqlmi.md)]

To monitor the performance of a database in Azure SQL Database and Azure SQL Managed Instance, start by monitoring the CPU and IO resources used by your workload relative to the level of database performance you chose in selecting a particular service tier and performance level. To accomplish this, Azure SQL Database and Azure SQL Managed Instance emit resource metrics that can be viewed in the Azure portal or by using one of these SQL Server management tools:

 - [Azure Data Studio](/sql/azure-data-studio/what-is), based on [Visual Studio Code](https://code.visualstudio.com/).
 - [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) (SSMS), based on [Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/).

| Monitoring solution | SQL Database | SQL Managed Instance | Requires agent on a customer-owned VM |  
|:--|:--|:--| 
| [Query Performance Insight](#generate-intelligent-assessments-of-performance-issues) | **Yes** | No | No |
| [Monitor using DMVs](monitoring-with-dmvs.md) | **Yes** | **Yes** | No |
| [Monitor using query store](/sql/relational-databases/performance/monitoring-performance-by-using-the-query-store)  | **Yes** | **Yes** | No |
| [SQL Insights (preview)](/azure/azure-monitor/insights/sql-insights-overview) in [Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) | **Yes** |  **Yes** | **Yes** | 
| [Azure SQL Analytics (preview)](/azure/azure-monitor/insights/azure-sql) using [Azure Monitor Logs](/azure/azure-monitor/logs/data-platform-logs) \* | **Yes** | **Yes** | No |

\* For solutions requiring low latency monitoring, Azure SQL Analytics (preview) is not recommended.

## Database advisors in the Azure portal 

Azure SQL Database provides a number of Database Advisors to provide intelligent performance tuning recommendations and automatic tuning options to improve performance. 

Additionally, the [Query Performance Insight](query-performance-insight-use.md) page shows you details about the queries responsible for the most CPU and IO usage for single and pooled databases. 

 - Query Performance Insight is available in the Azure portal in the Overview pane of your Azure SQL Database under "Intelligent Performance". Use the automatically collected information to identify queries and begin optimizing your workload performance. 
 - You can also configure [automatic tuning](automatic-tuning-overview.md) to implement these recommendations automatically, such as forcing a query execution plan to prevent regression, or creating and dropping nonclustered indexes based on workload patterns. Automatic tuning also is available in the Azure portal in the Overview pane of your Azure SQL Database under "Intelligent Performance".

Azure SQL Database and Azure SQL Managed Instance provide advanced monitoring and tuning capabilities backed by artificial intelligence to assist you in troubleshooting and maximizing the performance of your databases and solutions. You can choose to configure the [streaming export](metrics-diagnostic-telemetry-logging-streaming-export-configure.md#diagnostic-telemetry-for-export) of these [Intelligent Insights](intelligent-insights-overview.md) and other database resource logs and metrics to one of several destinations for consumption and analysis. 

Outside of the Azure portal, the database engine has its own monitoring and diagnostic capabilities that Azure SQL Database and SQL Managed Instance leverage, such as [query store](/sql/relational-databases/performance/monitoring-performance-by-using-the-query-store) and [dynamic management views (DMVs)](/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views). See [Monitoring using DMVs](monitoring-with-dmvs.md) for scripts to monitor for a variety of performance issues in Azure SQL Database and Azure SQL Managed Instance.

### Azure SQL Insights (preview) and Azure SQL Analytics (preview)

Both offerings use different pipelines to present data to a variety of endpoints for coming Azure SQL Database metrics. 

- [Azure SQL Insights (preview)](/azure/azure-monitor/insights/sql-insights-overview) is project inside Azure Monitor that can provide advanced insights into Azure SQL database activity. It is deployed via a customer-managed VM using Telegraf as a collection agent that connects to SQL sources, collects data, and moves data into Log Analytics.

- [Azure SQL Analytics (preview)](/azure/azure-monitor/insights/azure-sql) also requires Log Analytics to provide advanced insights into Azure SQL database activity.

- Azure diagnostic telemetry is a separate, streaming source of data for Azure SQL Database and Azure SQL Managed Instance. Not to be confused with the Azure SQL Insights (preview) product, SQLInsights is a log inside Intelligent Insights, and is one of several packages of telemetry emitted by Azure diagnostic settings. Diagnostic settings are a feature that contains Resource Log categories (formerly known as Diagnostic Logs). For more information, see [Diagnostic telemetry for export](metrics-diagnostic-telemetry-logging-streaming-export-configure.md?tabs=azure-portal#diagnostic-telemetry-for-export).
    - Azure SQL Analytics (preview) consumes the resource logs coming from the diagnostic telemetry (configurable under **Diagnostic Settings** in the Azure portal), while Azure SQL Insights (preview) uses a different pipeline to collect Azure SQL telemetry.

### Monitoring and diagnostic telemetry

The following diagram details all the database engine, platform metrics, resource logs, and Azure activity logs generated by Azure SQL products, how they are processed, and how they can be surfaced for analysis.

:::image type="content" source="media/monitor-tune-overview/azure-sql-insights-horizontal-analytics-full-diagram.svg" alt-text="Diagram showing complete logging and diagnostic information paths for Azure SQL products.":::

## Monitor and tune Azure SQL in the Azure portal

In the Azure portal, Azure SQL Database and Azure SQL Managed Instance provide monitoring of resource metrics. Azure SQL Database provides database advisors, and Query Performance Insight provides query tuning recommendations and query performance analysis. In the Azure portal, you can enable automatic tuning for [logical SQL servers](logical-servers.md) and their single and pooled databases.

> [!NOTE]
> Databases with extremely low usage may show in the portal with less than actual usage. Due to the way telemetry is emitted when converting a double value to the nearest integer certain usage amounts less than 0.5 will be rounded to 0 which causes a loss in granularity of the emitted telemetry. For details, see [Low database and elastic pool metrics rounding to zero](#low-database-and-elastic-pool-metrics-rounding-to-zero).

### Azure SQL Database and Azure SQL Managed Instance resource monitoring

You can quickly monitor a variety of resource metrics in the Azure portal in the **Metrics** view. These metrics enable you to see if a database is approaching the limits of CPU, memory, IO, or storage resources. High DTU, CPU or IO utilization may indicate that your workload needs more resources. It might also indicate that queries need to be optimized. See [Microsoft.Sql/servers/databases](/azure/azure-monitor/essentials/metrics-supported#microsoftsqlserversdatabases), [Microsoft.Sql/servers/elasticPools](/azure/azure-monitor/essentials/metrics-supported#microsoftsqlserverselasticpools) and [Microsoft.Sql/managedInstances](/azure/azure-monitor/essentials/metrics-supported#microsoftsqlmanagedinstances) for supported metrics in Azure SQL Database and Azure SQL Managed Instance.

  ![Resource metrics](./media/monitor-tune-overview/resource-metrics.png)

### Database advisors in Azure SQL Database

Azure SQL Database includes [database advisors](database-advisor-implement-performance-recommendations.md) that provide performance tuning recommendations for single and pooled databases. These recommendations are available in the Azure portal as well as by using [PowerShell](/powershell/module/az.sql/get-azsqldatabaseadvisor). You can also enable [automatic tuning](automatic-tuning-overview.md) so that Azure SQL Database can automatically implement these tuning recommendations.

### Query Performance Insight in Azure SQL Database

[Query Performance Insight](query-performance-insight-use.md) shows the performance in the Azure portal of top consuming and longest running queries for single and pooled databases.

### Low database and elastic pool metrics rounding to zero

Starting in September 2020, databases with extremely low usage may show in the portal with less than actual usage. Due to the way telemetry is emitted when converting a double value to the nearest integer certain usage amounts less than 0.5 will be rounded to 0, which causes a loss in granularity of the emitted telemetry.

For example: Consider a 1-minute window with the following four data points: 0.1, 0.1, 0.1, 0.1, these low values are rounded down to 0, 0, 0, 0 and present an average of 0. If any of the data points are greater than 0.5, for example: 0.1, 0.1, 0.9, 0.1, they are rounded to 0, 0, 1, 0 and show an avg of 0.25.

## Generate intelligent assessments of performance issues

[Intelligent Insights](intelligent-insights-overview.md) for Azure SQL Database and Azure SQL Managed Instance uses built-in intelligence to continuously monitor database usage through artificial intelligence and detect disruptive events that cause poor performance. Intelligent Insights automatically detects performance issues with databases based on query execution wait times, errors, or time-outs. Once detected, a detailed analysis is performed by Intelligent Insights that generates a resource log called SQLInsights (unrelated to the [Azure Monitor SQL Insights (preview)](monitoring-sql-database-azure-monitor.md)). SQLInsights is an [intelligent assessment of the issues](intelligent-insights-troubleshoot-performance.md). This assessment consists of a root cause analysis of the database performance issue and, where possible, recommendations for performance improvements.

Intelligent Insights is a unique capability of Azure built-in intelligence that provides the following value:

- Proactive monitoring
- Tailored performance insights
- Early detection of database performance degradation
- Root cause analysis of issues detected
- Performance improvement recommendations
- Scale out capability on hundreds of thousands of databases
- Positive impact to DevOps resources and the total cost of ownership

## Enable the streaming export of metrics and resource logs

You can enable and configure the [streaming export of diagnostic telemetry](metrics-diagnostic-telemetry-logging-streaming-export-configure.md#diagnostic-telemetry-for-export) to one of several destinations, including the Intelligent Insights resource log.

You configure diagnostic settings to stream categories of metrics and resource logs for single databases, pooled databases, elastic pools, managed instances, and instance databases to one of the following Azure resources.

### Log Analytics workspace in Azure Monitor

You can stream metrics and resource logs to a [Log Analytics workspace in Azure Monitor](/azure/azure-monitor/essentials/resource-logs#send-to-log-analytics-workspace). Data streamed here can be consumed by [SQL Analytics (preview)](/azure/azure-monitor/insights/azure-sql), which is a cloud only monitoring solution that provides intelligent monitoring of your databases that includes performance reports, alerts, and mitigation recommendations. Data streamed to a Log Analytics workspace can be analyzed with other monitoring data collected and also enables you to leverage other Azure Monitor features such as alerts and visualizations.

> [!NOTE]
> Azure SQL Analytics (preview) is an integration with Azure Monitor, where many monitoring solutions are no longer in active development. [Monitor your SQL deployments with SQL Insights (preview)](/azure/azure-monitor/insights/sql-insights-overview).

### Azure Event Hubs

You can stream metrics and resource logs to [Azure Event Hubs](/azure/azure-monitor/essentials/resource-logs#send-to-azure-event-hubs). Streaming diagnostic telemetry to event hubs to provide the following functionality:

- **Stream logs to third-party logging and telemetry systems**

  Stream all of your metrics and resource logs to a single event hub to pipe log data to a third-party SIEM or log analytics tool.
- **Build a custom telemetry and logging platform**

  The highly scalable publish-subscribe nature of event hubs allows you to flexibly ingest metrics and resource logs into a custom telemetry platform. For more information, see [Azure Event Hubs](/azure/event-hubs/event-hubs-about).
- **View service health by streaming data to Power BI**

  Use Event Hubs, Stream Analytics, and Power BI to transform your diagnostics data into near real-time insights on your Azure services. See [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](/azure/stream-analytics/stream-analytics-power-bi-dashboard) for details on this solution.

### Azure Storage

Stream metrics and resource logs to [Azure Storage](/azure/azure-monitor/essentials/resource-logs#send-to-azure-storage). Use Azure storage to archive vast amounts of diagnostic telemetry for a fraction of the cost of the previous two streaming options.

## Use Extended Events 

Additionally, you can use [Extended Events](/sql/relational-databases/extended-events/extended-events) for advanced monitoring and troubleshooting in SQL Server, Azure SQL Database, and Azure SQL Managed Instance. Extended Events is a "tracing" tool and event architecture, superior to SQL Trace, that enables users to collect as much or as little data as is necessary to troubleshoot or identify a performance problem, while mitigating impact to ongoing application performance. Extended Events replace deprecated SQL Trace and SQL Server Profiler features. For information about using extended events in Azure SQL Database, see [Extended events in Azure SQL Database](xevent-db-diff-from-svr.md). In Azure SQL Database and SQL Managed Instance, use an [Event File target hosted in Azure Blob Storage](xevent-code-event-file.md).

## Next steps

- For more information about intelligent performance recommendations for single and pooled databases, see [Database advisor performance recommendations](database-advisor-implement-performance-recommendations.md).
- For more information about automatically monitoring database performance with automated diagnostics and root cause analysis of performance issues, see [Azure SQL Intelligent Insights](intelligent-insights-overview.md).
- [Monitor your SQL deployments with SQL Insights (preview)](/azure/azure-monitor/insights/sql-insights-overview)
- [Monitor Azure SQL Database with Azure Monitor](monitoring-sql-database-azure-monitor.md)
- [Monitor Azure SQL Managed Instance with Azure Monitor](../managed-instance/monitoring-sql-managed-instance-azure-monitor.md)
