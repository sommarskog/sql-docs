---
title: "Online Restore: read-write file (full recovery model)"
description: This example shows an online restore in SQL Server of a read-write file for a database using the full recovery model with multiple filegroups.
author: MashaMSFT
ms.author: mathoma
ms.date: "12/17/2019"
ms.service: sql
ms.subservice: backup-restore
ms.topic: conceptual
helpviewer_keywords:
  - "full recovery model [SQL Server], RESTORE example"
  - "online restores [SQL Server], full recovery model"
  - "restore sequences [SQL Server], online"
---
# Example: Online Restore of a Read-Write File (Full Recovery Model)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  This topic is relevant for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] databases under the full recovery model that contain multiple files or filegroups.  
  
 In this example, a database named `adb`, which uses the full recovery model, contains three filegroups. Filegroup `A` is read/write, and filegroup `B` and filegroup `C` are read-only. Initially, all of the filegroups are online.  
  
 File `a1` in filegroup `A` appears to be damaged, and the database administrator decides to restore it while the database remains online.  
  
> [!NOTE]  
>  Under the simple recovery model, online restore of read/write data is not allowed.  
  
## Restore Sequences  
  
> [!NOTE]  
>  The syntax for an online restore sequence is the same as for an offline restore sequence.  
  
1.  Online restore of file `a1`.  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     At this point, file a1 is in the RESTORING state, and filegroup A is offline.  
  
2.  After restoring the file, the database administrator takes a new log backup to make sure that the point at which the file went offline is captured.  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  Online restore of log backups.  
  
     The administrator restores all the log backups taken since the restored file backup, ending with the latest log backup (*log_backup3*, taken in step 2). After the last backup is restored, the database is recovered.  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE DATABASE adb WITH RECOVERY;  
    ```  
  
     File `a1` is now online.  
  
## Additional Examples  
  
-   [Example: Piecemeal Restore of Database &#40;Simple Recovery Model&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Example: Piecemeal Restore of Only Some Filegroups &#40;Simple Recovery Model&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Example: Online Restore of a Read-Only File &#40;Simple Recovery Model&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Example: Piecemeal Restore of Database &#40;Full Recovery Model&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Example: Piecemeal Restore of Only Some Filegroups &#40;Full Recovery Model&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Example: Online Restore of a Read-Only File &#40;Full Recovery Model&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## See Also  
 [Online Restore &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Piecemeal Restores &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Restore and Recovery Overview &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Apply Transaction Log Backups &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
