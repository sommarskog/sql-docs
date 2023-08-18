---
title: "Agents (Transactional - SSMS)"
description: Describes the 'Agents' tab for a selected Transactional Publication within SQL Server Management Studio (SSMS).
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/07/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.monitor.publicationinfo.downlevelagents.tran.f1"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# Publication Information, Agents (Transactional Publication)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  The **Agents** tab displays summary information on the agents for the selected publication. Information on the Snapshot Agent and Log Reader Agent is displayed for all transactional publications. Information on the Queue Reader Agent is displayed for those transactional publications that are enabled for queued updating subscriptions.  
  
## Options  
 For more detailed information and tasks related to an agent, right-click the row for that agent, and then click an option on the shortcut menu. To change the way that the grid displays data, right-click the grid, and then click one of the following options:  
  
-   **Sort**: Sort on one or more columns in the **Sort Columns** dialog box.  
  
-   **Choose Columns to Show**: Select which columns to display and the order in which to display them in the **Choose Columns** dialog box.  
  
-   **Filter**: Filter rows in the grid based on column values in the **Filter Settings** dialog box.  
  
-   **Clear Filter**: Clear any filter settings for the grid.  
  
 Filter settings are specific to each grid. Column selection and sorting are applied to all grids of the same type, such as the publications grid for each Publisher.  
  
 **Status**  
 The status of each replication agent associated with the publication. The following list shows the possible status values:  
  
-   Error  
  
-   Retrying failed commands  
  
-   Not running  
  
-   Running  
  
-   Completed  
  
 **Agent**  
 The name of each replication agent associated with the publication. The Distribution Agent is associated with subscriptions to this publication. For more information, see [View Information and Perform Tasks using Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Last Start Time**  
 The last time the agent started.  
  
 **Duration**  
 The amount of time the agent has run. The time represents elapsed time if the agent is currently running and total time if the agent has run previously.  
  
 **Last Action**  
 The last action performed during the most recent run of the agent.  
  
## See Also  
 [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [View Information and Perform Tasks using Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
