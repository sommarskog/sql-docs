---
title: "Make Partial Updates to FILESTREAM Data"
description: Discover how to use the FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT value to make partial updates to FILESTREAM BLOB data. View an example of a partial update.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: filestream
ms.topic: conceptual
helpviewer_keywords:
  - "FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT"
  - "FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT"
---
# Make Partial Updates to FILESTREAM Data
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  An application uses FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT to make partial updates to FILESTREAM BLOB data. The [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) function passes this value and the handle that is returned from [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) to the FILESTREAM driver. The driver then forces a server-side copy of the current FILESTREAM data into the file that is referenced by the handle. If the application issues the FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT value after the handle has been written to, the last write operation persists and previous write operations that were made to the handle are lost.  
  
> [!NOTE]  
>  FILESTREAM relies on the [SMB protocol](/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview) for remote access.  
  
## Example  
 The following example shows you how to use the `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` value to perform a partial update of an inserted FILESTREAM BLOB.  
  
> [!NOTE]  
>  This example requires the FILESTREAM-enabled database and table that are created in [Create a FILESTREAM-Enabled Database](../../relational-databases/blob/create-a-filestream-enabled-database.md) and [Create a Table for Storing FILESTREAM Data](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## See Also  
 [Access FILESTREAM Data with OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Create Client Applications for FILESTREAM Data](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
