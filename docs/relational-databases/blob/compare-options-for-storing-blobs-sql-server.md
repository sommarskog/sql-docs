---
title: Compare Options for Storing Blobs (SQL Server)
description: SQL Server can store binary large object (blob) data used by Windows applications. Compare options in this relational database for storing unstructured data.
author: MikeRayMSFT
ms.author: mikeray
ms.date: 03/04/2019
ms.service: sql
ms.subservice: filestream
ms.topic: conceptual
---
# Compare Options for Storing Blobs (SQL Server)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Discusses and compares the options that are available for storing files and documents in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="Expectations"></a> Storing Files in the Database - Benefits and Expectations

A large percentage of enterprise data is unstructured in nature, and is typically stored as files and documents in file systems. Most of this data is produced, managed, and consumed by applications that access the files through Windows APIs. Enterprises typically keep this data in the file system, while storing the related metadata for the files in a relational database.

Integrating unstructured data into the relational database provides the following benefits:

- Integrated storage and data management capabilities such as backup.
- Integrated services such as full-text search and semantic search over data and metadata.
- Ease of administration and policy management over the unstructured data.

Generally it has been inconvenient to store unstructured data in a relational database. It has been impractical to rewrite established applications (such as Microsoft Word or Adobe Reader) to interact through relational database APIs. These applications expect the data to be accessible through Windows APIs. The applications have the following expectations:

- Windows applications are not aware of database transactions and do not require them.
- Windows applications require compatibility with file system APIs for file and directory data.

Many years ago, SQL Server did not offer any variety of ways to store unstructured data in a relational database. But nowadays it does offer ways to store unstructured data.

## <a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] already has the FILESTREAM feature. The FILESTREAM feature provides efficient storage, management, and streaming of unstructured data stored as files on the file system. However, a FILESTREAM solution requires custom programming, and does not satisfy the requirement for full Windows application compatibility described above.

## <a name="FileTables"></a> FileTables

The FileTable feature builds on top of existing FILESTREAM capabilities. The FileTable feature enables enterprise customers to store unstructured file data, and directory hierarchies, in a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. The feature addresses the requirements for non-transactional access and Windows application compatibility for file-based data.

## <a name="CompareFileTable"></a> Comparing FILESTREAM and FileTable

|Feature|File Server and Database Solution|FILESTREAM Solution|FileTable Solution|
|:------|:--------------------------------|:------------------|:-----------------|
|**Single story for management tasks**|No|Yes|**Yes**|
|**Single set of services**: search, reporting, querying, and so forth|No|Yes|**Yes**|
|**Integrated security model**|No|Yes|**Yes**|
|**In-place updates of FILESTREAM data**|Yes|No|**Yes**|
|**File and directory hierarchy maintained in the database**|No|No|**Yes**|
|**Windows application compatibility**|Yes|No|**Yes**|
|**Relational access to file attributes**|No|No|**Yes**|

## <a name="CompareRBS"></a> Comparing FILESTREAM and Remote BLOB Store (RBS)

Another option for storing unstructured data involves a Remote BLOB Store (RBS). For more information, see [Remote Blob Store (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md).

## <a name="more"></a> More Information

[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
[Remote Blob Store &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
