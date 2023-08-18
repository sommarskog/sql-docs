---
title: "Select Backup Device"
description: For SQL Server restore, use the Select Backup Device dialog box to select a logical backup device for the restore operation.
author: MashaMSFT
ms.author: mathoma
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: backup-restore
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.selectbackupdevice.f1"
---
# Select Backup Device
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use the **Select Backup Device** dialog box to select a logical backup device for the restore operation.  
  
 A logical backup device is a user-defined logical device that corresponds to a physical device, either a tape drive or a disk drive, that is provided by the operating system.  
  
> [!NOTE]  
>  If a backup uses multiple backup devices, they all must correspond to a single type of device.  
  
 **To use SQL Server Management Studio to view the contents of a backup device**  
  
-   [View the Contents of a Backup Tape or File &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [View the Properties and Contents of a Logical Backup Device &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## Options  
 **Backup device**  
 In the list box, select the name of a logical backup device from which you want to restore.  
  
 For information about how to view the contents of a backup device, see [View the Properties and Contents of a Logical Backup Device &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## Remarks  
 If you do not see a logical backup device that contains the backup you are seeking on the list, the backup might have been written directly to one or more files or tape drives. If this is the case, cancel the **Select Backup Device** dialog box; and in the **Specify Backup** dialog box, select **File** or **Tape** in the **Backup media** list box.  
  
## See Also  
 [Backup Devices &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
