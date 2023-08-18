---
title: "Replication Conflict Viewer (Peer-to-Peer)"
description: Learn about the Replication Conflict Viewer and how to use it to view conflicts for Peer-to-Peer Transactional Replication and Transactional Replication with queued updating subscriptions.
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.replconflictviewer.cvqueued.f1"
monikerRange: "=azuresqldb-current||>=sql-server-2016"
---
# Replication Conflict Viewer (Transactional Replication)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  The Replication Conflict Viewer enables you to view conflicts that have occurred during synchronization for peer-to-peer transactional replication and transactional replication with queued updating subscriptions. For more information, see [View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
> [!NOTE]  
>  The Replication Conflict Viewer displays conflicts that occur in merge replication and in transactional replication. For transactional replication, you can use Replication Conflict Viewer to view conflict data, but you cannot choose a different resolution for the conflict.  
  
## Options  
 The Replication Conflict Viewer is divided into two sections. The upper section of the dialog box shows the conflict list for the selected table. When you click an item in the conflict list, the details of the conflict are displayed in the lower section of the dialog box.  
  
 The conflict data in the lower section is displayed in two corresponding columns (**Conflict Winner** and **Conflict Loser**). If the conflict is between updated and deleted data, there may be no data to show for the deleted side of the conflict. In this case, the Replication Conflict Viewer displays a message in one of the columns, indicating the row was deleted at one location and updated at another. It also indicates the suggested resolution.  
  
 **Database**  
 Choose a database that includes publications with conflicts.  
  
 **Publication**  
 Choose a publication that includes tables with conflicts.  
  
 **Table**  
 Choose a table that includes conflicts.  
  
 **Define Filter**  
 Click to open the **Define Filters** dialog box.  
  
 **Apply or Remove Filter**  
 Click to apply or remove a filter that has been defined in the **Define Filters** dialog box.  
  
 **Select All**  
 Click to select all conflicts listed in the grid.  
  
 **Select None**  
 Click to deselect all conflicts listed in the grid.  
  
 **Remove**  
 Click to remove selected conflicts from the viewer and their associated metadata from the replication system tables.  
  
 **Show all columns**  
 Select to show all columns of the table.  
  
 **Show first five columns and other columns with conflicting data**  
 Select to display the first five columns and any columns that have conflicts. This is helpful when the table has a large number of columns, but you want to see only the columns most relevant to resolving the conflict. The first five columns are always included in this view, as fields that identify a row, such as the primary key or name fields, are often among the first columns of the table.  
  
 **Display Column Information** (**…**)  
 Click to view column information: **Table Name**, **Column Name**, **Data Type**, and **Column Value**.  
  
 **Log the details of the conflict**  
 Check this box to log the details of the conflict to a file. To specify a location for the file, point to the **View** menu and click **Options**. Enter a value, or click the browse (**...**) and navigate to the appropriate file. Click **OK** to exit the **Options** dialog box.  
  
## See Also  
 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
