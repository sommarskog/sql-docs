---
title: "View backup contents (file or tape)"
description: This article shows you how to view the content of a backup tape or file in SQL Server by using SQL Server Management Studio or Transact-SQL.
author: MashaMSFT
ms.author: mathoma
ms.date: "12/17/2019"
ms.service: sql
ms.subservice: backup-restore
ms.topic: conceptual
helpviewer_keywords:
  - "backup devices [SQL Server], tapes"
  - "displaying backup content"
  - "viewing backup content"
  - "tape backup devices, viewing contents"
  - "database backups [SQL Server], viewing content"
  - "backing up databases [SQL Server], viewing content"
---
# View the contents of a backup tape or file (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  This topic describes how to view the content of a backup tape or file in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  Support for tape backup devices will be removed in a future version of SQL Server. Avoid using this feature in new development work, and plan to modify applications that currently use this feature.  
  
 **In This Topic**  
  
-   **Before you begin:**  
  
     [Security](#Security)  
  
-   **To view the content of a backup tape or file, using:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
###  <a name="Security"></a> Security  
 For information about security, see [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
####  <a name="Permissions"></a> Permissions  
 In [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later versions, obtaining information about a backup set or backup device requires CREATE DATABASE permission. For more information, see [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To view the content of a backup tape or file  
  
1.  After connecting to the appropriate instance of the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], in Object Explorer, click the server name to expand the server tree.  
  
2.  Expand **Databases**, and, depending on the database, either select a user database or expand **System Databases** and select a system database.  
  
3.  Right-click the database you want to backup, point to **Tasks**, and then click **Back Up**. The **Back Up Database** dialog box appears.  
  
4.  In the **Destination** section of the **General** page, click either **Disk** or **Tape**. In the **Back up to** list box, look for the disk file or tape you want.  
  
     If the disk file or tape is not displayed in the list-box, click **Add**. Select a file name or tape drive. To add it to the **Back up to** list-box, click **OK**.  
  
5.  In the **Back up to** list-box, select the path of the disk or tape drive you want to view, and click **Contents**. This opens the **Device Contents** dialog box.  
  
6.  The right-hand pane displays information about the media set and backup sets on the selected tape or file.  
  
##  <a name="TsqlProcedure"></a> Using Transact-SQL  
  
#### To view the content of a backup tape or file  
  
1.  Connect to the [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  From the Standard bar, click **New Query**.  
  
3.  Use the [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) statement. This example returns information about the file named `AdventureWorks2022-FullBackup.bak`.  
  
```sql  
USE AdventureWorks2022;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2022-FullBackup.bak' ;  
GO  
```  
  
## See Also  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [Backup Devices &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Define a Logical Backup Device for a Disk File &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Define a Logical Backup Device for a Tape Drive &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
