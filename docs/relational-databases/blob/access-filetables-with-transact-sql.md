---
title: "Access FileTables with Transact-SQL"
description: Learn how Transact-SQL data manipulation language (DML) commands work with FileTables. See which system-defined constraints are enforced during DML operations.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: filestream
ms.topic: conceptual
helpviewer_keywords:
  - "FileTables [SQL Server], accessing files with T-SQL"
---
# Access FileTables with Transact-SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Describes how [!INCLUDE[tsql](../../includes/tsql-md.md)] data manipulation language (DML) commands work with FileTables.  
  
##  <a name="BasicsInsert"></a> INSERT Operations on FileTables  
 The following considerations apply to **INSERT** Operations on FileTables:  
  
-   All the file attribute columns have NOT NULL constraints. If values are not explicitly set, then appropriate default values are supplied.  
  
-   System-defined constraints are enforced if the INSERT statement sets the **name**, **path_locator**, **parent_path_locator**, or file attributes.  
  
-   The application can obtain the **path_locator** for a file or directory by providing the file system path to the [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) function.  
  
##  <a name="BasicsUpdate"></a> UPDATE Operations on FileTables  
 The following considerations apply to **UPDATE** operations on FileTables:  
  
-   Updates to any user-defined data are allowed.  
  
-   System-defined constraints are enforced if the INSERT statement sets the **name**, **path_locator**, **parent_path_locator**, or file attributes.  
  
-   Updates can be made to the FILESTREAM data in the **file_stream** column without affecting any of the other columns, including the timestamps.  
  
##  <a name="BasicsDelete"></a> DELETE Operations on FileTables  
 The following considerations apply to **DELETE** operations on FileTables:  
  
-   Deleting a row also removes the corresponding file or directory from the file system.  
  
-   Deleting a row fails if the row corresponds to a directory that contains other files or directories.  
  
##  <a name="BasicsConstraints"></a> Constraints That Are Enforced for DML Operations on FileTables  
 System-defined constraints ensure that DML actions do not compromise the integrity of the file namespace hierarchy. The constraints that are enforced include the following:  
  
-   When you set or change the **name** of the file or directory:  
  
    -   Windows file and directory naming conventions are enforced.  
  
    -   The uniqueness of the name in the parent directory is enforced.  
  
-   When you set or change the location of a file or directory by setting or changing the **path_locator** or **parent_path_locator**:  
  
    -   Uniqueness is enforced.  
  
    -   The consistency of the hierarchical tree of directories and files is enforced, including the consistency of **path_locator** and **parent_path_locator** values.  
  
-   The value of **is_directory** cannot be set to true when the **file_stream** column is not null. Data in the **file_stream** column indicates that the row represents a file and not a directory.  
  
-   File attribute columns cannot be null. NOT NULL constraints are enforced with default values.  
  
-   The value of **last_access_time** cannot be earlier than **last_write_time** and **creation_time**.  
  
## See Also  
 [Load Files into FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Access FileTables with File Input-Output APIs](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
