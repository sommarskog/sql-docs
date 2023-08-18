---
author: MashaMSFT
ms.author: mathoma
ms.reviewer: randolphwest
ms.date: 07/06/2023
ms.topic: include
---
| Error | Severity | Event logged | Description |
| :--- | :--- | :--- | :--- |
| 5001 | 16 | No | User must be in the master database. |
| 5002 | 16 | No | Database '%.\*ls' does not exist. Verify the name in sys.databases and try the operation again. |
| 5003 | 16 | No | Database mirroring cannot be enabled while the database has offline files. |
| 5004 | 16 | No | To use ALTER DATABASE, the database must be in a writable state in which a checkpoint can be executed. |
| 5005 | 16 | No | Specified recovery time of %I64d seconds is less than zero or more than the maximum of %d seconds. |
| 5006 | 16 | No | Could not get exclusive use of %S_MSG '%.\*ls' to perform the requested operation. |
| 5008 | 16 | No | This ALTER DATABASE statement is not supported. Correct the syntax and execute the statement again. |
| [5009](../mssqlserver-5009-database-engine-error.md) | 16 | No | One or more files listed in the statement could not be found or could not be initialized. |
| 5010 | 16 | No | Log file name cannot be generated from a raw device. The log file name and path must be specified. |
| 5011 | 14 | No | User does not have permission to alter database '%.\*ls', the database does not exist, or the database is not in a state that allows access checks. |
| 5012 | 16 | No | The name of the primary filegroup cannot be changed. |
| 5013 | 16 | No | The master and model databases cannot have files added to them. ALTER DATABASE was aborted. |
| 5014 | 16 | No | The %S_MSG '%.\*ls' does not exist in database '%.\*ls'. |
| 5015 | 16 | No | ALTER DATABASE failed. The total size specified must be 1 MB or greater. |
| 5016 | 16 | No | Cannot change the name of the system database %.\*ls. |
| 5017 | 16 | No | The AUTOGROW_ALL_FILES or AUTOGROW_SINGLE_FILE property cannot be modified on a FILESTREAM or MEMORY_OPTIMIZED_DATA filegroup. |
| 5018 | 10 | No | The file "%.\*ls" has been modified in the system catalog. The new path will be used the next time the database is started. |
| 5019 | 10 | No | Cannot find entry in sys.master_files for file '%.\*ls'. |
| 5020 | 16 | No | The primary data or log file cannot be removed from a database. |
| 5021 | 10 | No | The %S_MSG name '%.\*ls' has been set. |
| 5022 | 16 | No | Log file '%ls' for this database is already active. |
| 5023 | 16 | No | The database must be suspect or in emergency mode to rebuild the log. |
| 5024 | 16 | No | No entry found for the primary log file in sysfiles1. Could not rebuild the log. |
| 5025 | 16 | No | The file '%ls' already exists. It should be renamed or deleted so that a new log file can be created. |
| 5027 | 16 | No | System databases master, model, and tempdb cannot have their logs rebuilt. |
| 5028 | 16 | No | The system could not activate enough of the database to rebuild the log. |
| 5029 | 10 | Yes | Warning: The log for database '%.\*ls' has been rebuilt. Transactional consistency has been lost. The RESTORE chain was broken, and the server no longer has context on the previous log files, so you will need to know what they were. You should run DBCC CHECKDB to validate physical consistency. The database has been put in dbo-only mode. When you are ready to make the database available for use, you will need to reset database options and delete any extra log files. |
| 5030 | 16 | No | The database %.\*ls could not be exclusively locked to perform the operation. |
| 5031 | 16 | No | Cannot remove the file '%.\*ls' because it is the only file in the DEFAULT filegroup. |
| 5032 | 10 | No | The file cannot be shrunk below page %d until the log is backed up because it contains bulk logged pages. |
| 5033 | 16 | No | The maximum of %ld files per database has been exceeded. |
| 5034 | 16 | No | The file %ls is currently being autogrown or modified by another process. Try the operation again later. |
| 5035 | 16 | No | Filegroup '%.\*ls' already exists in this database. Specify a different name or remove the conflicting filegroup if it is empty. |
| 5036 | 16 | No | MODIFY FILE failed. Specify logical name. |
| 5038 | 16 | No | MODIFY FILE failed for file "%.\*ls". At least one property per file must be specified. |
| 5039 | 16 | No | MODIFY FILE failed. Specified size is less than or equal to current size. |
| 5040 | 16 | No | MODIFY FILE failed for database '%.\*ls', file id %d. Size of file (%I64d KB) is greater than MAXSIZE (%I64d KB). |
| 5041 | 16 | No | MODIFY FILE failed. File '%.\*ls' does not exist. |
| 5042 | 16 | No | The %S_MSG '%.\*ls' cannot be removed because it is not empty. |
| 5043 | 16 | No | The %S_MSG '%.\*ls' cannot be found in %ls. |
| 5044 | 10 | No | The %S_MSG '%.\*ls' has been removed. |
| 5045 | 16 | No | The %S_MSG already has the '%ls' property set. |
| 5046 | 10 | No | The %S_MSG property '%ls' has been set. |
| 5047 | 16 | No | Cannot change the READONLY property of the PRIMARY filegroup. |
| 5048 | 16 | No | Cannot add, remove, or modify files in filegroup '%.\*ls'. The filegroup is read-only. |
| 5050 | 16 | No | Cannot change the properties of empty filegroup '%.\*ls'. The filegroup must contain at least one file. |
| 5051 | 16 | No | Cannot have a filegroup with the name 'DEFAULT'. |
| 5052 | 16 | No | %ls is not permitted while a database is in the %ls state. |
| 5054 | 16 | No | Could not cleanup worktable IAM chains to allow shrink or remove file operation. Please try again when tempdb is idle. |
| 5055 | 16 | No | Cannot add, remove, or modify file '%.\*ls'. The file is read-only. |
| 5056 | 16 | No | Cannot add, remove, or modify a file in filegroup '%.\*ls' because the filegroup is not online. |
| 5057 | 16 | No | Cannot add, remove, or modify file '%.\*ls' because it is offline. |
| 5058 | 16 | No | Option '%.\*ls' cannot be set in database '%.\*ls'. |
| 5059 | 16 | No | Database '%.\*ls' is in transition. Try the ALTER DATABASE statement later. |
| 5060 | 10 | No | Nonqualified transactions are being rolled back. Estimated rollback completion: %d%%. |
| 5061 | 16 | No | ALTER DATABASE failed because a lock could not be placed on database '%.\*ls'. Try again later. |
| 5062 | 16 | No | The option "%.\*ls" conflicts with another requested option. The options cannot both be requested at the same time. |
| 5063 | 16 | No | Database '%.\*ls' is in warm standby. A warm-standby database is read-only. |
| 5064 | 16 | No | Changes to the state or options of database '%.\*ls' cannot be made at this time. The database is in single-user mode, and a user is currently connected to it. |
| 5065 | 16 | No | The file "%ls" is currently being scanned or used by a background or user process. Try the operation again later. |
| 5066 | 16 | No | Database options single user and dbo use only cannot be set at the same time. |
| 5067 | 16 | No | The database option TORN_PAGE_DETECTION is incompatible with the PAGE_CHECKSUM option. |
| 5068 | 10 | No | Failed to restart the current database. The current database is switched to master. |
| 5069 | 16 | No | ALTER DATABASE statement failed. |
| 5070 | 16 | No | Database state cannot be changed while other users are using the database '%.\*ls' |
| 5071 | 16 | No | Rebuild log can only specify one file. |
| 5072 | 16 | No | ALTER DATABASE failed. The default collation of database '%.\*ls' cannot be set to %.\*ls. |
| 5073 | 16 | No | Cannot alter collation for database '%ls' because it is READONLY, OFFLINE, or marked SUSPECT. |
| 5074 | 16 | No | The %S_MSG '%.\*ls' is dependent on %S_MSG '%.\*ls'. |
| 5075 | 16 | No | The %S_MSG '%.\*ls' is dependent on %S_MSG. The database collation cannot be changed if a schema-bound object depends on it. Remove the dependencies on the database collation and then retry the operation. |
| 5076 | 10 | No | Warning: Changing default collation for database '%.\*ls', which is used in replication. All replication databases should have the same default collation. |
| 5077 | 16 | No | Cannot change the state of non-data files or files in the primary filegroup. |
| 5078 | 16 | No | Cannot alter database options for "%ls" because it is READONLY, OFFLINE, or marked SUSPECT. |
| 5079 | 10 | No | Database "%.\*ls" is %S_MSG for vardecimal storage format. |
| 5080 | 16 | No | Vardecimal storage format cannot be disabled for database "%.\*ls" because the database is not under simple recovery model. Change the database recovery model to simple and then reissue the command. |
| 5081 | 16 | No | The value for change tracking option '%ls' is not valid. The value must be a positive number. |
| 5082 | 16 | No | Cannot change the versioning state on database "%.\*ls" together with another database state. |
| 5083 | 16 | No | The termination option is not supported when making versioning state changes. |
| 5084 | 10 | Yes | Setting database option %ls to %ls for database '%.\*ls'. |
| 5085 | 16 | No | Alter database command failed because SQL Server was started with one or more undocumented trace flags that prevent enabling/disabling database for versioning. |
| 5086 | 16 | No | Cannot disable vardecimal storage format for database "%.\*ls" because there are one or more tables that have vardecimal storage format enabled. Disable the vardecimal storage format on all tables before disabling the vardecimal storage format for the database. |
| 5087 | 16 | No | The file content type mismatches with the content type of the filegroup. |
| 5088 | 16 | No | Change tracking is already enabled for database '%.\*ls'. |
| 5089 | 16 | No | Change tracking is disabled for database '%.\*ls'. Change tracking must be enabled on a database to modify change tracking settings. |
| 5090 | 16 | No | Database '%.\*ls' is a system database. Change tracking settings cannot be modified for system databases. |
| 5091 | 15 | No | ALTER DATABASE change tracking option '%ls' was specified more than once. Each option can be specified only once. |
| 5092 | 15 | No | The value for change tracking option '%ls' is not valid. The value must be between %d and %d minutes. |
| 5093 | 16 | No | The operation cannot be performed on a database snapshot. |
| 5094 | 16 | No | The operation cannot be performed on a database with database snapshots or active DBCC replicas. |
| 5095 | 16 | No | A database or filegroup cannot be set to read-only mode when any files are subject to a RESTORE PAGE operation. Complete the restore sequence involving file "%ls" before attempting to transition to read-only. |
| 5096 | 16 | No | The recovery model cannot be changed to SIMPLE when any files are subject to a RESTORE PAGE operation. Complete the restore sequence involving file "%ls" before attempting to transition to SIMPLE. |
| 5097 | 16 | No | The container cannot be set to the offline state because changes exist that require a log backup. Take a log backup and then retry the ALTER DATABASE statement. |
| 5098 | 16 | No | The container can not be dropped because changes exist that require a log backup. Take a log backup and then retry the ALTER DATABASE operation. |
| 5099 | 16 | No | ALTER DATABASE failed because the READ_COMMITTED_SNAPSHOT and the ALLOW_SNAPSHOT_ISOLATION options cannot be set to ON when a database has FILESTREAM filegroups. To set READ_COMMITTED_SNAPSHOT or ALLOW_SNAPSHOT_ISOLATION to ON, you must remove the FILESTREAM filegroups from the database. |
| 5102 | 22 | No | Attempted to open a filegroup for the invalid ID %d in database "%.\*ls". |
| 5103 | 16 | No | MAXSIZE cannot be less than SIZE for file '%ls'. |
| 5104 | 16 | No | File '%.\*ls' already used. |
| 5105 | 16 | Yes | A file activation error occurred. The physical file name '%.\*ls' may be incorrect. Diagnose and correct additional errors, and retry the operation. |
| 5108 | 10 | No | Log file '%.\*ls' does not match the primary file. It may be from a different database or the log may have been rebuilt previously. |
| 5110 | 16 | No | The file "%.\*ls" is on a network path that is not supported for system database files. |
| 5111 | 10 | No | File activation failure. The physical file name "%.\*ls" may be incorrect. |
| 5112 | 10 | Yes | FCB::SetSize dbid %d fileid %d oldSize %d newSize %d. To prevent this informational message from appearing in the error log, use DBCC TRACEOFF to turn off the trace flag. |
| 5113 | 10 | No | The log cannot be rebuilt because there were open transactions/users when the database was shutdown, no checkpoint occurred to the database, or the database was read-only. This error could occur if the transaction log file was manually deleted or lost due to a hardware or environment failure. |
| 5114 | 16 | No | Log files, offline files, restoring files, and defunct files for database snapshots should not be specified. "%.\*ls" is not an eligible file for a database snapshot. |
| 5115 | 16 | No | Only SQL Server database files can be specified for database snapshots. '%.\*ls' is not a SQL Server database file. |
| 5118 | 16 | No | The file "%ls" is compressed but does not reside in a read-only database or filegroup. The file must be decompressed. |
| 5119 | 16 | No | Cannot make the file "%.\*ls" a sparse file. Make sure the file system supports sparse files. |
| [5120](../mssqlserver-5120-database-engine-error.md) | 16 | No | Unable to open the physical file "%.\*ls". Operating system error %d: "%ls". |
| 5121 | 16 | No | The path specified by "%.\*ls" is not in a valid directory. |
| 5123 | 16 | No | CREATE FILE encountered operating system error %ls while attempting to open or create the physical file '%.\*ls'. |
| 5124 | 16 | Yes | The file header in '%ls' does not match the expected contents for file '%ls' of database '%ls'. The mismatch is possibly between the full-text catalog files and the related database. Perform a restore if necessary. |
| 5125 | 24 | No | File '%ls' appears to have been truncated by the operating system. Expected size is %I64d KB but actual size is %I64d KB. |
| 5127 | 16 | No | All files must be specified for database snapshot creation. Missing the file "%ls". |
| 5128 | 17 | No | Write to sparse file '%ls' failed due to lack of disk space. |
| 5129 | 10 | No | The log cannot be rebuilt when the primary file is read-only. |
| 5130 | 10 | No | The log cannot be rebuilt when database mirroring is enabled. |
| 5131 | 10 | No | The log was not rebuilt because there is more than one log file. |
| 5132 | 16 | No | The path specified by '%.\*ls' cannot be used for FILESTREAM files because it is a raw device. |
| 5133 | 16 | No | Directory lookup for the file "%ls" failed with the operating system error %ls. |
| 5134 | 16 | No | The path that is specified by '%.\*ls' cannot be used for FILESTREAM files because it is not on a supported file system. |
| 5135 | 16 | No | The path '%.\*ls' cannot be used for FILESTREAM files. For information about supported paths, see SQL Server Books Online. |
| 5136 | 16 | No | The path specified by '%.\*ls' cannot be used for a FILESTREAM container since it is contained in another FILESTREAM container. |
| 5137 | 16 | No | Snapshot database file and base database file are not allowed to be on the different type of storage. |
| 5138 | 16 | No | Trailing space is not allowed in SQL file name '%.\*ls' on cloud storage. |
| 5139 | 16 | No | Operation (%.\*ls) failed on '%.\*ls'. Operating system error %d: "%ls" |
| 5140 | 16 | No | Failed to lock credential object (Account: %.\*ls, Container: %.\*ls). Lock Mode: %.\*ls. |
| 5141 | 16 | No | Failed to lock credential manager. Lock Mode: %.\*ls. |
| 5142 | 16 | No | Failed to lock lease renewal manager. Lock Mode: %.\*ls. |
| 5143 | 16 | No | Concurrent operation (%.\*ls) failed on file '%.\*ls'. Operating system error %d: "%ls" |
| 5144 | 10 | Yes | Autogrow of file '%.\*ls' in database '%.\*ls' was cancelled by user or timed out after %d milliseconds. Use ALTER DATABASE to set a smaller FILEGROWTH value for this file or to explicitly set a new file size. |
| 5145 | 10 | Yes | Autogrow of file '%.\*ls' in database '%.\*ls' took %d milliseconds. Consider using ALTER DATABASE to set a smaller FILEGROWTH for this file. |
| 5149 | 16 | No | MODIFY FILE encountered operating system error %ls while attempting to expand the physical file '%ls'. |
| 5150 | 16 | No | The size of a single log file must not be greater than 2 TB. |
| 5152 | 16 | No | This operation is not supported for URL %.\*ls. |
| 5153 | 16 | No | OVERFLOW is not supported in Alter Database modify statement in Sql DW back door. |
| 5159 | 24 | No | Operating system error %.\*ls on file "%.\*ls" during %ls. |
| 5161 | 16 | Yes | An unexpected file id was encountered. File id %d was expected but %d was read from "%.\*ls". Verify that files are mapped correctly in sys.master_files. ALTER DATABASE can be used to correct the mappings. |
| 5169 | 16 | No | FILEGROWTH cannot be greater than MAXSIZE for file '%.\*ls'. |
| 5170 | 16 | Yes | Cannot create file '%ls' because it already exists. Change the file path or the file name, and retry the operation. |
| 5171 | 16 | No | %.\*ls is not a primary database file. |
| 5172 | 16 | No | The header for file '%ls' is not a valid database file header. The %ls property is incorrect. |
| 5173 | 16 | Yes | One or more files do not match the primary file of the database. If you are attempting to attach a database, retry the operation with the correct files. If this is an existing database, the file may be corrupted and should be restored from a backup. |
| 5174 | 16 | No | Each file size must be greater than or equal to 512 KB. |
| 5175 | 10 | Yes | The file %.\*ls has been expanded to allow recovery to succeed. After recovery completes, you can increase the size of the files in the database. Contact the system administrator for assistance. |
| 5176 | 10 | Yes | To allow recovery to succeed, the log file '%.\*ls' has been expanded beyond its maximum size. After recovery completes, you should either increase the size of the log file in the database or schedule more frequent backups of the log (under the full or bulk-logged recovery model). |
| 5177 | 16 | Yes | An unexpected error occurred while checking the sector size for file '%.\*ls'. Move the file to a local NTFS volume, where the sector size can be retrieved. Check the SQL Server error log for more information. |
| 5178 | 16 | Yes | Cannot use file '%.\*ls' because it was originally formatted with sector size %d and is now on a volume with sector size %d. Move the file to a volume with a sector size that is the same as or smaller than the original sector size. |
| 5179 | 16 | Yes | Cannot use file '%.\*ls', because it is on a volume with sector size %d. SQL Server supports a maximum sector size of 4096 bytes. Move the file to a volume with a compatible sector size. |
| [5180](../mssqlserver-5180-database-engine-error.md) | 22 | Yes | Could not open File Control Block (FCB) for invalid file ID %d in database '%.\*ls'. Verify the file location. Execute DBCC CHECKDB. |
| 5181 | 16 | No | Could not restart database "%.\*ls". Reverting to the previous status. |
| 5182 | 10 | Yes | New log file '%.\*ls' was created. |
| 5183 | 16 | No | Cannot create the file "%ls". Use WITH MOVE to specify a usable physical file name. Use WITH REPLACE to overwrite an existing file. |
| 5184 | 16 | No | Cannot use file '%.\*ls' for clustered server. Only formatted files on which the cluster resource of the server has a dependency can be used. Either the disk resource containing the file is not present in the cluster group or the cluster resource of the Sql Server does not have a dependency on it. |
| 5185 | 16 | No | Cannot find the matching log file for FILESTRAM file '%.\*ls'. |
| 5186 | 16 | No | Encountered an error (NT status code 0x%x) while attempting to start the Transactional File System Resource Manager '%.\*ls'. |
| 5188 | 16 | No | Encountered error (NT status code 0x%x) while attempting to perform redo for transactional file system resource manager '%.\*ls'. |
| 5189 | 16 | No | Encountered error (NT status code 0x%x) while attempting to perform undo for transactional file system resource manager '%.\*ls'. |
| 5190 | 16 | No | Encountered error (NT status code 0x%x) while attempting to checkpoint transactional file system resource manager '%.\*ls'. |
| 5191 | 10 | No | Local directory '%.\*ls' is used for tempdb in a clustered server. This directory must exist on each cluster node and SQL Server service has read/write permission on it. |
| 5192 | 16 | No | Maximum allowed file size is %I64dGB. |
| 5193 | 21 | No | Failed to access file due to lease mismatch. Bringing down database. |
| 5194 | 16 | No | The size for FILESTREAM log file '%.\*ls' must be greater than or equal to 1 MB. |
| 5195 | 16 | No | The Cluster Service function call '%s' failed with error code '%s' while verifying the file path. Verify that your failover cluster is configured properly. |
| 5196 | 10 | No | The file "%ls" has been uncompressed. |
| 5197 | 16 | No | Encountered an error (%ls) while attempting to uncompress the file "%ls". |
| 5198 | 16 | No | The path specified by "%.\*ls" is a UNC path. UNC path is not supported in failover clustered environment. |
| 5199 | 16 | No | The path specified by "%.\*ls" is a raw device. Raw device path is not supported in failover clustered environment. |
| 5201 | 10 | No | DBCC SHRINKDATABASE: File ID %d of database ID %d was skipped because the file does not have enough free space to reclaim. |
| 5202 | 10 | No | DBCC SHRINKDATABASE for database ID %d is waiting for the snapshot transaction with timestamp %I64d and other snapshot transactions linked to timestamp %I64d or with timestamps older than %I64d to finish. |
| 5203 | 10 | No | DBCC SHRINKFILE for file ID %d is waiting for the snapshot transaction with timestamp %I64d and other snapshot transactions linked to timestamp %I64d or with timestamps older than %I64d to finish. |
| 5204 | 16 | No | Could not find allocation unit ID %I64d. Check sys.allocation_units. |
| 5205 | 10 | No | %.\*ls: Moving page %d:%d failed. |
| 5206 | 10 | No | %.\*ls: Page %d:%d could not be moved because it could not be read. |
| 5207 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is a work table page. |
| 5208 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is a work file page. |
| 5209 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is a dedicated allocation page. |
| 5210 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is an invalid page type. |
| 5211 | 10 | No | %.\*ls: Page %d:%d could not be moved because it was deallocated during shrink. |
| 5212 | 10 | No | %.\*ls: System table SYSFILES1 Page %d:%d could not be moved to other files because it only can reside in the primary file of the database. |
| 5213 | 10 | No | %.\*ls: Page %d:%d could not be moved because its ownership was changed during shrink. |
| 5214 | 10 | No | %.\*ls: Page %d:%d could not be moved because its page type was changed during shrink. |
| 5215 | 10 | No | %.\*ls: Page %d:%d could not be moved because the partition to which it belonged was dropped or is part of a paused resumable index build. Use sys.index_resumable_operations to identify paused resumable index builds. |
| 5216 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because the table to which it belonged was dropped. |
| 5217 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is an empty non-leaf level index page. |
| 5218 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because the table name could not be found. |
| 5219 | 10 | No | %.\*ls: Heap page %d:%d could not be moved. |
| 5220 | 10 | No | %.\*ls: Index Allocation Map (IAM) page %d:%d could not be moved. |
| 5221 | 10 | No | %.\*ls: Index Allocation Map (IAM) page %d:%d from a dropped allocation unit could not be moved. |
| 5222 | 10 | No | %.\*ls: Page %d:%d from a dropped allocation unit could not be deallocated. |
| 5223 | 10 | No | %.\*ls: Empty page %d:%d could not be deallocated. |
| 5224 | 10 | No | %.\*ls: Empty large object page %d:%d could not be deallocated. |
| 5225 | 10 | No | %.\*ls: Not all ghost records on the large object page %d:%d could be removed. If there are active queries on readable secondary replicas check the current ghost cleanup boundary. |
| 5226 | 10 | No | %.\*ls: Page %d:%d (type UNLINKED_REORG_PAGE) could not be deallocated. |
| 5227 | 10 | No | %.\*ls: Page %d:%d (type BULK_OPERATION_PAGE) could not be deallocated. |
| [5228](../mssqlserver-5228-database-engine-error.md) | 16 | No | Table error: object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls), page %S_PGID, row %d. DBCC detected incomplete cleanup from an online index build operation. (The anti-matter column value is %d.) |
| [5229](../mssqlserver-5229-database-engine-error.md) | 16 | No | Table error: Object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls) contains an anti-matter column, but is not a nonclustered index. |
| 5230 | 10 | No | The check statement was aborted. DBCC CHECKCATALOG cannot be run on TEMPDB. |
| [5231](../mssqlserver-5231-database-engine-error.md) | 10 | No | Object ID %ld (object '%.\*ls'): A deadlock occurred while trying to lock this object for checking. This object has been skipped and will not be processed. |
| 5232 | 10 | No | DBCC CHECKDB will not check SQL Server catalog or Service Broker consistency because a database snapshot could not be created or because WITH TABLOCK was specified. |
| [5233](../mssqlserver-5233-database-engine-error.md) | 16 | No | Table error: alloc unit ID %I64d, page %S_PGID. The test (%.\*ls) failed. The values are %ld and %ld. |
| 5234 | 10 | No | DBCC SHRINKDATABASE: File ID %d of database ID %d was skipped because trying to adjust the space allocation for the file was failed. |
| [5235](../mssqlserver-5235-database-engine-error.md) | 10 | No | %lsDBCC %ls (%ls%ls%ls)%ls executed by %ls terminated abnormally due to error state %d. Elapsed time: %d hours %d minutes %d seconds. |
| 5236 | 10 | No | Unable to process object '%ls' because it is a four-part name, which is not supported by any DBCC command. |
| [5237](../mssqlserver-5237-database-engine-error.md) | 10 | No | DBCC cross-rowset check failed for object '%.\*ls' (object ID %d) due to an internal query error. |
| 5238 | 16 | No | Unable to process object ID %ld (object '%.\*ls') because it is a stored procedure or user-defined function, which is not supported by any DBCC command. |
| 5239 | 16 | No | Unable to process object ID %ld (object '%.\*ls') because this DBCC command does not support objects of this type. |
| 5240 | 10 | No | File ID %d of database ID %d cannot be shrunk as it is either being shrunk by another process or is empty. |
| 5241 | 10 | No | File ID %d of database ID %d cannot be shrunk as the target shrink size (%I64d KB) is greater than the actual file size (%I64d KB). |
| [5242](../mssqlserver-5242-database-engine-error.md) | 16 | No | An inconsistency was detected during an internal operation in database '%.\*ls'(ID:%d) on page %S_PGID. Please contact technical support. |
| [5243](../mssqlserver-5243-database-engine-error.md) | 16 | No | An inconsistency was detected during an internal operation. Please contact technical support. |
| 5244 | 16 | No | Repair statement not processed. One or more files in the database are read-only and must be made writeable in order to run repair. |
| [5245](../mssqlserver-5245-database-engine-error.md) | 16 | No | Object ID %ld (object '%.\*ls'): DBCC could not obtain a lock on this object because the lock request timeout period was exceeded. This object has been skipped and will not be processed. |
| 5246 | 16 | No | Repair operations cannot be performed on the MSSQLSYSTEMRESOURCE database. Consult Books Online topic "Resource Database" for more information. |
| 5247 | 16 | No | Repair: insert a secondary index row based on its base table row. |
| 5248 | 10 | No | Repair: Successfully %ls row in index "%ls" in database "%ls". |
| 5249 | 10 | No | %.\*ls: Page %d:%d could not be moved because shrink could not lock the page. |
| [5250](../mssqlserver-5250-database-engine-error.md) | 16 | No | Database error: %ls page %S_PGID for database '%.\*ls' (database ID %d) is invalid. This error cannot be repaired. You must restore from backup. |
| 5251 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because maintaining NC indexes associated with the heap failed. |
| 5252 | 10 | No | File ID %d of database ID %d cannot be shrunk to the expected size. The high concurrent workload is leading to too many deadlocks during the shrink operation. Re-run the shrink operation when the workload is lower. |
| 5253 | 10 | No | The check statement was aborted. DBCC CHECKALLOC cannot be run on TEMPDB. |
| 5254 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because the table to which it belonged was building the heap by another process. |
| 5255 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is a sort page. |
| [5256](../mssqlserver-5256-database-engine-error.md) | 16 | No | Table error: alloc unit ID %I64d, page %S_PGID contains an incorrect page ID in its page header. The PageId in the page header = %S_PGID. |
| 5257 | 10 | No | %.\*ls: File ID %d of database ID %d was skipped because the file size was changed in the middle of shrink operation. |
| 5258 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because building computed column expression failed. |
| 5259 | 10 | No | %.\*ls: Heap page %d:%d could not be moved because populating computed column expression failed. |
| 5260 | 16 | No | Object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls): At least one record on page %S_PGID contains versioning information, but the VERSION_INFO bit in the page header is not set. |
| 5261 | 10 | No | %.\*ls: Page %d:%d could not be moved because it has not been formatted. |
| 5262 | 16 | No | Object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls), page %S_PGID, row %d: Row contains a NULL versioning timestamp, but its version chain pointer is not NULL. Version chain points to page %S_PGID, slot %d. |
| 5263 | 10 | No | Found incorrect count(s) for table '%.\*ls', index '%.\*ls', partition %ld: |
| 5264 | 10 | No | DATA pages %.\*ls: From system table - %I64d pages; Actual - %I64d pages. |
| 5265 | 10 | No | USED pages %.\*ls: From system table - %I64d pages; Actual - %I64d pages. |
| 5266 | 10 | No | RSVD pages %.\*ls: From system table - %I64d pages; Actual - %I64d pages. |
| 5267 | 10 | No | ROWS count: From system table - %I64d rows; Actual - %I64d rows. |
| 5268 | 10 | No | DBCC %.\*ls is performing an exhaustive search of %d indexes for possible inconsistencies. This is an informational message only. No user action is required. |
| 5269 | 16 | No | Check terminated. The transient database snapshot for database '%.\*ls' (database ID %d) has been marked suspect due to an IO operation failure. Refer to the SQL Server error log for details. |
| 5270 | 10 | No | %.\*ls: Page %d:%d could not be moved because it is an unmovable page in a critical system table. |
| 5271 | 10 | No | DBCC %ls could not output results for this command due to an internal failure. Review other errors for details. |
| 5272 | 10 | No | %.\*ls: Index Allocation Map (IAM) page %d:%d could not be moved because the underlying object could not be accessed exclusively. |
| 5273 | 10 | No | %.\*ls: Page %d:%d could not be moved because it belonged to an index/heap that was/is in build online. |
| 5274 | 16 | No | Table error: Object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls), page %S_PGID. %S_MSG is invalid for compressed page; the following internal test failed: %.\*ls. Values are %ld and %ld. |
| 5275 | 10 | No | Exhaustive search of '%.\*ls' (database ID %d) for inconsistencies completed. Processed %d of %d total searches. Elapsed time: %I64d milliseconds. This is an informational message only. No user action is required. |
| 5276 | 10 | No | Exhaustive search of '%.\*ls' (database ID %d) for inconsistencies failed due to exception %d, state %d. This is an informational message only. No user action is required. |
| 5277 | 10 | No | Internal %lsdatabase snapshot has split point LSN = %08x:%08x:%04x and first LSN = %08x:%08x:%04x. |
| 5278 | 10 | No | DBCC encountered a page with an LSN greater than the current end of log LSN %S_LSN for its internal database snapshot. Could not read page %S_PGID, database '%.\*ls' (database ID %d), LSN = %S_LSN, type = %ld, isInSparseFile = %d. Please re-run this DBCC command." |
| 5279 | 16 | No | Table error: object ID %d, index ID %d, partition ID %I64d, database fragment ID %d. The row on page (%d:%d), slot ID %d should be on fragment ID %d but was found in fragment ID %d. |
| 5280 | 16 | No | An unexpected protocol element was received during the execution of a consistency check command. Retry the operation. |
| 5281 | 10 | No | Estimated TEMPDB space (in KB) needed for %s on database %.\*ls = %I64d. |
| 5282 | 16 | No | Table error: Object ID %d, index ID %d, partition ID %I64d, alloc unit ID %I64d (type %.\*ls), page %S_PGID. The header of the page is invalid: the IS_IN_SYSXACT flag bit is set. |
| 5283 | 10 | No | The Cross Rowset check on nonclustered columnstore index object ID %d, index ID %d, partition number %d failed. Please rebuild the partition. |
| 5284 | 16 | No | The replicated index '%.\*ls' (object ID %d) and one or more of its clones do not contain the same rows. |
| 5285 | 16 | No | Nonclustered columnstore index '%.\*ls' on table '%.\*ls' has a missing dictionary on column id %d and rowgroup id %d. Drop and recreate the nonclustered columnstore index. |
| 5286 | 10 | No | %.\*ls: Page %d:%d could not be moved because it belongs to an active online index build with LOBs. |
| 5287 | 10 | No | DBCC THROWERROR bypass exception. This is an informational message only. No user action is required. |
| 5288 | 16 | No | Columnstore index has one or more data values that do not match data values in a dictionary. Please run DBCC CHECKDB for more info. |
| 5289 | 16 | No | Clustered columnstore index '%.\*ls' column '%.\*ls' rowgroup id %d on table '%.\*ls' has one or more data values that do not match data values in a dictionary. Restore the data from a backup. |
| 5290 | 16 | No | Columnstore index has one or more data values that are inconsistent with data values within the metadata. Please run DBCC CHECKDB for more info. |
| 5291 | 16 | No | Clustered columnstore index '%.\*ls' column '%.\*ls' rowgroup id %d on table '%.\*ls' has one or more data values that are inconsistent with data values within the metadata. Restore the data from a backup. |
| 5292 | 16 | No | Column store index '%.\*ls' on table '%.\*ls' has erroneous content in its Delete Bitmap with rowgroup_id %d and tuple_id %d. |
| 5293 | 16 | No | Nonclustered columnstore index '%.\*ls' column '%.\*ls' rowgroup id %d on table '%.\*ls' has one or more data values that do not match data values in a dictionary. Drop and recreate the nonclustered columnstore index. |
| 5294 | 16 | No | Nonclustered columnstore index '%.\*ls' column '%.\*ls' rowgroup id %d on table '%.\*ls' has one or more data values that are inconsistent with data values within the metadata. Drop and recreate the nonclustered columnstore index. |
| 5295 | 16 | No | DBCC UPDATEUSAGE cannot acquire lock on object 'sysallocunits'. Please try again later. |
| 5296 | 10 | No | Object ID %ld (object '%.\*ls'): The operation is not supported with memory optimized tables. This object has been skipped and will not be processed. |
| 5297 | 10 | No | The Cross Rowset check between clustered columnstore index and nonclustered index (object ID %d, index ID %d, partition number %d) failed. Please rebuild the partition. |
| 5298 | 16 | No | Cannot display content of page %S_PGID. The rowset it belongs to is in tombstone state and pending removal. |
| 5299 | 16 | No | Query Store Error:%d State:%d Message:%.\*ls |
| 5301 | 16 | No | Bulk load failed. User does not have ALTER TABLE permission on table '%.\*ls'. ALTER TABLE permission is required on the target table of a bulk load if the target table contains triggers or check constraints, but the 'FIRE_TRIGGERS' or 'CHECK_CONSTRAINTS' bulk hints are not specified. ALTER TABLE permission is also required if the 'KEEPIDENTITY' bulk hint is specified. |
| 5302 | 16 | No | Mutator '%.\*ls' on '%.\*ls' cannot be called on a null value. |
| 5303 | 16 | No | The result of applying mutator '%.\*ls' on CLR type '%.\*ls' cannot be a null value. |
| 5304 | 16 | No | Bulk copy failed. User does not have ALTER TABLE permission on table '%.\*ls'. ALTER TABLE permission is required on the target table of a bulk copy operation if the table has triggers or check constraints, but 'FIRE_TRIGGERS' or 'CHECK_CONSTRAINTS' bulk hints are not specified as options to the bulk copy command. |
| 5305 | 16 | No | The rowdump and lockres columns are only valid on tables and indexed views on which the NOEXPAND hint is specified. |
| 5306 | 16 | No | Cursor parameters are not allowed for functions. Variable '%.\*ls' is of type cursor. |
| 5307 | 16 | No | Invalid parameter specified for sp_cursoropen. |
| 5308 | 16 | No | Windowed functions, aggregates and NEXT VALUE FOR functions do not support integer indices as ORDER BY clause expressions. |
| 5309 | 16 | No | Windowed functions, aggregates and NEXT VALUE FOR functions do not support constants as ORDER BY clause expressions. |
| 5310 | 16 | No | Aggregates are not allowed in the VALUES list of an INSERT statement. |
| 5311 | 16 | No | Invalid quote character '%lc'. A remote server or user command used an invalid quote character. |
| 5312 | 16 | No | The input to the function 'ntile' cannot be bound. |
| 5313 | 16 | No | Synonym '%.\*ls' refers to an invalid object. |
| 5314 | 16 | No | The use of aggregates is not allowed in this context. |
| 5315 | 16 | No | The target of a MERGE statement cannot be a remote table, a remote view, or a view over remote tables. |
| 5316 | 16 | No | The target '%.\*ls' of the MERGE statement has an INSTEAD OF trigger on some, but not all, of the actions specified in the MERGE statement. In a MERGE statement, if any action has an enabled INSTEAD OF trigger on the target, then all actions must have enabled INSTEAD OF triggers. |
| 5317 | 16 | No | The target of a MERGE statement cannot be a partitioned view. |
| 5318 | 16 | No | In a MERGE statement, the source and target cannot have the same name or alias. Use different aliases for the source and target to ensure that they have unique names in the MERGE statement. |
| 5319 | 16 | No | Aggregates are not allowed in a WHEN clause of a MERGE statement. |
| 5321 | 16 | No | The '%ls' function is not allowed in the %S_MSG clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5322 | 16 | No | An aggregate function is not allowed in the %S_MSG clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5323 | 15 | No | Subqueries are not allowed in the %S_MSG clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5324 | 15 | No | In a MERGE statement, a '%S_MSG' clause with a search condition cannot appear after a '%S_MSG' clause with no search condition. |
| 5325 | 15 | No | The order of the data in the data file does not conform to the ORDER hint specified for the BULK rowset '%.\*ls'. The order of the data must match the order specified in the ORDER hint for a BULK rowset. Update the ORDER hint to reflect the order in which the input data is ordered, or update the input data file to match the order specified by the ORDER hint. |
| 5326 | 15 | No | The data in the data file does not conform to the UNIQUE hint specified for the BULK rowset '%.\*ls'. The data in the data file must be unique if the UNIQUE hint is specified for a BULK rowset. Remove the UNIQUE hint, or update the input data file to ensure that the data is unique. |
| 5327 | 15 | No | The column '%.\*ls' does not have a valid data type for the ORDER hint specified for data source '%.\*ls'. The text, ntext, image, xml, varchar(max), nvarchar(max) and varbinary(max) data types cannot be used in the ORDER hint for a BULK rowset or CLR TVF. |
| 5328 | 15 | No | Cannot insert explicit value for the identity column '%.\*ls' in the target table '%.\*ls' of the INSERT statement when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5329 | 15 | No | Windowed functions are not allowed in the %S_MSG clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5330 | 16 | No | Full-text predicates cannot appear in the OUTPUT clause. |
| 5331 | 16 | No | Full-text predicates cannot appear in the %S_MSG clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 5332 | 15 | No | The order of the data in the stream does not conform to the ORDER hint specified for the CLR TVF '%.\*ls'. The order of the data must match the order specified in the ORDER hint for a CLR TVF. Update the ORDER hint to reflect the order in which the input data is ordered, or update the CLR TVF to match the order specified by the ORDER hint. |
| 5333 | 16 | No | The identifier '%.\*ls' cannot be bound. Only source columns and columns in the clause scope are allowed in the 'WHEN NOT MATCHED' clause of a MERGE statement. |
| 5334 | 16 | No | The identifier '%.\*ls' cannot be bound. Only target columns and columns in the clause scope are allowed in the 'WHEN NOT MATCHED BY SOURCE' clause of a MERGE statement. |
| 5335 | 16 | No | The data type %ls cannot be used as an operand to the UNION, INTERSECT or EXCEPT operators because it is not comparable. |
| 5336 | 16 | No | Recursive references are not allowed on the right hand side of an EXCEPT operator in the recursive part of recursive CTEs. |
| 5337 | 16 | No | A constant folding error caused the creation or alteration of the %S_MSG to fail. Common causes for this error are arithmetic overflow, type conversion failure, and divide-by-zero in an expression in the %S_MSG. |
| 5338 | 16 | No | Format option cannot be specified together with SINGLE_BLOB, SINGLE_CLOB or SINGLE_NCLOB option. |
| 5339 | 16 | No | CSV format option is supported for char and widechar datafiletype options. |
| 5340 | 16 | No | WITH schema clause cannot be specified together with FORMATFILE or SINGLE_BLOB/SINGLE_CLOB/SINGLE_NCLOB option. |
| 5341 | 16 | No | WITH schema clause cannot be provided without FORMAT = 'CSV' option. |
| 5342 | 16 | No | ROWTERMINATOR and FIELDTERMINATOR/DELIMITER cannot be provided without WITH schema. |
| 5343 | 16 | No | ROWTERMINATOR and FIELDTERMINATOR/DELIMITER can only be used with schema inference or WITH clause. |
| 5344 | 16 | No | Duplicate column ordinal cannot be provided in WITH schema clause. |
| 5345 | 16 | No | Both OFFSET and LENGTH parameters have to be provided together with inline schema (WITH clause). |
| 5346 | 16 | No | DATAFILETYPE can only be used with schema inference or WITH clause. |
| 5347 | 16 | No | USE_TYPE_DEFAULT option cannot be provided without WITH schema. |
| 5348 | 16 | No | An ERRORFILE_SECRET cannot be specified together with ERRORFILE_DATA_SOURCE option. |
| 5349 | 16 | No | An ERRORFILE_SECRET cannot be specified without ERRORFILE option. |
| 5350 | 16 | No | CSV format supports only TABLESAMPLE PERCENT option. |
| 5351 | 16 | No | Partial file cannot be provided together with TABLESAMPLE clause. |
| 5352 | 16 | No | Missing update assignment in update with action hint. |
| 5353 | 16 | No | Parser version '%ls' is not supported for provided format '%ls'. |
| 5354 | 16 | No | Parser version '%ls' is not supported. |
| 5355 | 16 | No | Empty string value cannot be provided as '%ls' option for specified format '%ls' and PARSER_VERSION '%ls'. |
| 5356 | 16 | No | Specifying database or server credential is not supported for OPENROWSET. |
| 5357 | 16 | No | Option '%ls' is not supported for specified format '%ls' and PARSER_VERSION '%ls'. |
| 5358 | 16 | No | An ERRORFILE_LOCATION cannot be specified without ERRORFILE_DATA_SOURCE option. |
| 5359 | 16 | No | An ERRORFILE_DATA_SOURCE cannot be specified without ERRORFILE_LOCATION option. |
| 5360 | 16 | No | With clause, format file and SINGLE_BLOB/SINGLE_CLOB/SINGLE_NCLOB options cannot be used with ReadMode=Metadata. |
| 5361 | 16 | No | Unsupported combination of datafiletype option and format. |
| 5362 | 15 | No | Window '%.\*ls' is undefined. |
| 5363 | 15 | No | The function '%.\*ls' may not have ORDER BY in OVER or WINDOW clause. |
| 5364 | 15 | No | Window frame with ROWS or RANGE must have an ORDER BY clause. |
| 5365 | 15 | No | Cyclic window references are not permitted. |
| 5366 | 15 | No | The function '%.\*ls' must have an OVER clause or a WINDOW with ORDER BY. |
| 5367 | 15 | No | Window specification defined in one window can not be redefined in another window. |
| 5368 | 16 | No | Option '%ls' is not supported for specified format '%ls'. |
| 5369 | 16 | No | Option '%ls' is not supported for locations with '%ls' connector when specified FORMAT is '%ls'. |
| 5370 | 16 | No | Invalid column reference detected in view '%.\*ls'. Please recreate the view or refresh the column definitions using sp_refreshview stored procedure. |
| 5371 | 16 | No | Connector prefix '%ls' is not supported for specified FORMAT '%ls'. |
| 5372 | 16 | No | The specified bulk option '%ls' is not supported for file format '%ls'. Review the documentation for supported options. |
| 5373 | 16 | No | All the input parameters should be of the same type. Supported types are tinyint, smallint, int, bigint, decimal and numeric. |
| 5374 | 16 | No | WITH clause is not supported for locations with '%ls' connector when specified FORMAT is '%ls'. |
| 5501 | 16 | No | The FILESTREAM filegroup was dropped before the table can be created. |
| 5502 | 16 | No | The FILESTREAM container is inaccessible. |
| 5503 | 10 | No | Unable to find entry in sys.database_files for FILESTREAM file '%.\*ls'. |
| 5504 | 15 | No | 'PRIMARY' can only be specified for FILESTREAM log filegroup in a 'CONTAINS' clause. |
| 5505 | 16 | No | A table that has FILESTREAM columns must have a nonnull unique column with the ROWGUIDCOL property. |
| 5506 | 15 | No | FILESTREAM data or log file cannot be named 'DEFAULT'. |
| 5507 | 15 | No | DEFAULT cannot be specified for FILESTREAM log filegroup '%.\*ls'. |
| 5508 | 15 | No | FILESTREAM can only be declared for VARBINARY columns. |
| 5509 | 15 | No | The properties SIZE or FILEGROWTH cannot be specified for the FILESTREAM data file '%.\*ls'. |
| 5510 | 15 | No | LOG ON cannot be used for non-FILESTREAM file group '%.\*ls'. |
| 5511 | 23 | No | FILESTREAM's file system log record '%.\*ls' under log folder '%.\*ls' is corrupted. |
| [5512](../mssqlserver-5512-database-engine-error.md) | 16 | Yes | Error 0x%x (%ls) was encountered while directory '%.\*ls' was being truncated. |
| 5513 | 16 | No | The name that is specified for the associated log filegroup for FILESTREAM filegroup '%.\*ls' is not valid. |
| 5514 | 16 | No | Transactional replication/Change Data Capture cannot proceed because Transactional File System Resource Manager at '%.\*ls' is not started. |
| [5515](../mssqlserver-5515-database-engine-error.md) | 20 | No | Cannot open the container directory '%.\*ls' of the FILESTREAM file. The operating system has returned the status code 0x%x. |
| 5516 | 16 | No | The FILESTREAM log filegroup '%.\*ls' cannot be referred to by more than one FILESTREAM data filegroup. |
| 5517 | 16 | No | FILESTREAM container MAXSIZE must be greater than or equal to 512 KB. |
| 5518 | 16 | No | FILESTREAM path '%.\*ls' is too long. |
| 5519 | 16 | No | A database must have primary FILESTREAM log filegroup and log file in order for it to contain other FILESTREAM filegroups. |
| 5520 | 16 | No | Upgrade of FILESTREAM container ID %d in the database ID %d failed because of container size recalculation error. Examine the previous errorlog entries for errors, and take the appropriate corrective actions. |
| 5521 | 16 | No | Error 0x%x (NT status code) was encountered when SQL Server attempts to retrieve '%.\*ls' from the Transaction File System Resource Manager located at '%.\*ls'. |
| 5522 | 16 | No | FILESTREAM data file cannot be removed because its log file has not been backed up. |
| 5523 | 16 | No | FILESTREAM data file group cannot be added to refer to an empty FILESTREAM log file group. |
| 5524 | 16 | No | Default FILESTREAM data filegroup cannot be removed unless it's the last FILESTREAM data filegroup left. |
| 5525 | 16 | No | The READ_ONLY and READ_WRITE property cannot be modified on a FILESTREAM log filegroup. |
| 5526 | 16 | No | The FILESTREAM log file '%.\*ls' cannot be removed because it is being referenced by a FILESTREAM data filegroup. |
| 5527 | 16 | No | The primary FILESTREAM log file cannot be dropped because other FILESTREAM filegroups exist. |
| 5528 | 16 | No | A database can have at most one primary FILESTREAM log filegroup and log file. |
| 5529 | 16 | No | Failed to remove a FILESTREAM file. The database is a primary database in an availability group. Wait for the FILESTREAM data files to be hardened on every secondary availability replica. Then retry the drop file operation. |
| 5531 | 16 | No | Error 0x%x (NT status code) was encountered when SQL Server attempts to change the logging mode of Transaction File System Resource Manager located at '%.\*ls' from '%.\*ls' to '%.\*ls'. |
| 5532 | 16 | No | SQL Server cannot obtain the Kernel Transaction Manager's transaction context to perform file system operation. |
| 5533 | 23 | No | The FILESTREAM file system log record that has the LSN '%d:%d:%d' is missing. Log folder '%.\*ls' is corrupted. Restore the database from a backup. |
| 5534 | 23 | No | SQL log record at LSN '%d:%d:%d' for database '%.\*ls' is corrupted. Database cannot recover. |
| 5535 | 23 | No | FILESTREAM data container '%.\*ls' is corrupted. Database cannot recover. |
| 5536 | 23 | No | FILESTREAM deleted folder '%.\*ls' is corrupted. Database cannot recover. |
| 5537 | 16 | No | Function %ls is only valid on columns with the FILESTREAM attribute. |
| 5538 | 16 | No | Partial updates are not supported on columns that have a FILESTREAM as a source. |
| 5539 | 16 | No | The ROWGUIDCOL column associated with the FILESTREAM being used is not visible where method %ls is called. |
| 5540 | 16 | No | The FILESTREAM column cannot be used with method %ls because the associated ROWGUIDCOL of the base table is nullable or does not have a unique constraint. |
| 5541 | 16 | No | An open mode must be used when a FILESTREAM column is opened as a file. |
| 5542 | 16 | No | The FILESTREAM filegroup '%.\*ls' has no files assigned to it. FILESTREAM data cannot be populated on this filegroup until a file is added. |
| 5543 | 10 | No | FILESTREAM: effective level = %d (remote access disabled), configured level = %d, file system access share name = '%.\*ls'. |
| 5544 | 10 | No | FILESTREAM: effective level = %d (remote access enabled), configured level = %d, file system access share name = '%.\*ls'. |
| 5545 | 10 | No | FILESTREAM: connected to kernel driver %ls. This is an informational message. No user action is required. |
| 5546 | 10 | No | FILESTREAM: failed to connect to kernel driver %ls. |
| 5550 | 16 | No | Too many Filestream containers were specified for Filestream Filegroup '%.\*ls'. Specifying more than one Filestream Container per Filestream Filegroup is not supported in this edition of SQL Server. See Books Online for more details on feature support in different SQL Server editions. |
| 5551 | 16 | No | FILESTREAM file '%.\*ls' cannot be added because its destination filegroup cannot have more than one file. Specifying more than one Filestream Container per Filestream Filegroup is not supported in this edition of SQL Server. See Books Online for more details on feature support in different SQL Server editions. |
| 5552 | 16 | No | FILESTREAM file named with GUID '%.\*ls' that belongs to FILESTREAM data file ID 0x%x does not exist or cannot be opened. |
| 5553 | 16 | No | SQL Server internal error. FILESTREAM manager cannot continue with current command. |
| [5554](../mssqlserver-5554-database-engine-error.md) | 16 | No | The total number of versions for a single file has reached the maximum limit set by the file system. |
| 5555 | 16 | No | The operation has failed because the FILESTREAM data cannot be renamed. |
| 5556 | 16 | No | The database '%.\*ls' does not exist or does not support FILESTREAM. Supply a valid database name. To see available databases, use sys.databases. |
| 5557 | 16 | No | The FILESTREAM container '%.\*ls' does not exist or cannot be processed. Supply a valid FILESTREAM container name. To see available containers, use sys.databases_files. |
| 5558 | 16 | No | Database '%.\*ls' should be in single-user mode. |
| 5559 | 16 | No | Could not open the database '%.\*ls'. |
| 5560 | 16 | No | Access to the FILESTREAM tombstone table for the database '%.\*ls' cannot be performed at the moment because it conflicts with another activity, such as background GC operation, backup operation, DBCC CHECK\* operation or on-going snapshot creation. |
| 5561 | 16 | No | FILESTREAM garbage collector operation was aborted on the database '%.\*ls'. |
| 5570 | 16 | No | FILESTREAM Failed to find the garbage collection table. |
| 5571 | 23 | No | Internal FILESTREAM error: failed to access the garbage collection table. |
| 5572 | 23 | No | Internal FILESTREAM error: failed to perform a filesystem operation because of a potential corruption. |
| 5573 | 10 | No | Internal FILESTREAM error: failed to access the tombstones table with HRESULT: 0x%x. |
| 5574 | 16 | No | A database cannot be enabled for both Database Mirroring and FILESTREAM or for both Database Mirroring and MEMORY_OPTIMIZED_DATA storage. |
| 5575 | 10 | No | Operation '%ls' failed with HRESULT: %ls in file '%hs', line %d while executing sp_filestream_configure. |
| 5576 | 10 | No | FILESTREAM feature is enabled. This is an informational message. No user action is required. |
| 5577 | 10 | No | FILESTREAM access level has been changed to %d. Restart the instance of SQL Server for the settings to fully take effect. |
| 5578 | 16 | No | A failure occurred while FILESTREAM configuration was being changed or applied. For more information, see the SQL Server error log. |
| 5579 | 10 | No | FILESTREAM: effective level = %d, configured level = %d. |
| 5580 | 16 | No | FILESTREAM InstanceGuid is null. Registry settings might be corrupted. |
| 5581 | 10 | No | FILESTREAM feature has been disabled. Restart the instance of SQL Server for the settings to fully take effect. If you have data in FILESTREAM columns, it will not be accessible after the SQL Server instance has been restarted. |
| 5582 | 10 | No | Machine reboot is required before the FILESTREAM feature settings can take effect. |
| 5583 | 16 | No | The specified value for the enable_level parameter of the sp_filestream_configure stored procedure is not valid. The value must be 0, 1, 2, or 3. |
| 5584 | 16 | No | Another session is executing the sp_filestream_configure stored procedure. Check the updated configuration settings and retry the operation if necessary. |
| 5585 | 10 | No | FILESTREAM file I/O access could not be enabled. The operating system Administrator must enable FILESTREAM file I/O access on the instance using Configuration Manager. |
| 5586 | 10 | No | The FILESTREAM feature is already configured to the specified level. No change has been made. |
| 5588 | 16 | No | Access to FILESTREAM data is not supported under snapshot isolation level. |
| 5589 | 16 | No | Access to FILESTREAM data is not supported under row versioning-based read committed snapshot isolation (RCSI). |
| 5590 | 16 | No | FILESTREAM operations are not supported on the platform. |
| 5591 | 16 | No | FILESTREAM feature is disabled. |
| 5592 | 16 | No | FILESTREAM feature doesn't have file system access enabled. |
| 5593 | 16 | No | FILESTREAM feature is not supported on WoW64. The feature is disabled. |
| 5594 | 16 | No | The value specified for the computer_name_format parameter of the .%ls() function is not valid. |
| 5595 | 16 | No | .PhysicalPathName is disabled. |
| 5596 | 10 | No | FILESTREAM feature configuration might be inconsistent. To reset the configuration, use the sp_configure stored procedure. |
| 5597 | 16 | No | FILESTREAM feature could not be initialized. The operating system Administrator must enable FILESTREAM on the instance using Configuration Manager. |
| 5598 | 10 | No | FILESTREAM feature is not supported on user instances. |
| 5599 | 16 | No | .ContainerId is disabled. |
| 5600 | 16 | No | The Cross Database Chaining option cannot be set to the specified value on the specified database. |
| 5601 | 16 | No | The service master key could not be force regenerated as requested by the -F startup option. The error number is %ld. |
| 5602 | 10 | No | The service master key regeneration was successful. |
| 5603 | 16 | No | The password for SA could not be force regenerated as requested by the -K startup option. The error number is %ld. |
| 5604 | 10 | No | The password regeneration attempt for SA was successful. |
| 5605 | 16 | No | The password for SA account could not be force regenerated and/or SA account cannot be disabled as requested by the -K startup option and the -T1617 trace flag. |
| 5701 | 10 | No | Changed database context to '%.\*ls'. |
| 5702 | 10 | No | SQL Server is terminating this process. |
| 5703 | 10 | No | Changed language setting to %.\*ls. |
| 5803 | 10 | No | Unknown configuration (id = %d) encountered in sys.configurations. |
| 5804 | 16 | Yes | Character set, sort order, or collation cannot be changed at the server level because at least one database is not writable. Make the database writable, and retry the operation. |
| 5805 | 16 | No | Too few locks specified. Minimum %d. |
| 5807 | 16 | No | Recovery intervals above %d minutes not recommended. Use the RECONFIGURE WITH OVERRIDE statement to force this configuration. |
| 5808 | 16 | No | Ad hoc update to system catalogs is not supported. |
| 5810 | 16 | No | Valid values for the fill factor are 0 to 100. |
| 5812 | 14 | No | You do not have permission to run the RECONFIGURE statement. |
| 5828 | 16 | No | User connections are limited to %d. |
| 5829 | 16 | No | The specified user options value is invalid. |
| 5831 | 16 | No | Minimum server memory value (%d) must be less than or equal to the maximum value (%d). |
| 5832 | 16 | No | The affinity mask specified does not match the CPU mask on this system. |
| 5833 | 16 | No | The affinity mask specified is greater than the number of CPUs supported or licensed on this edition of SQL Server. |
| 5834 | 16 | No | The affinity specified conflicts with the IO affinity mask specified. Change the affinity setting to use different CPUs than those specified in the IO affinity mask. |
| 5835 | 16 | No | Failed to start CPUs with the mask 0x%lx on the system. |
| 5836 | 16 | No | Lightweight pooling is not supported on this platform or in this edition of SQL Server. |
| 5837 | 16 | No | The service broker listen port cannot be dynamic. Valid port values are 1024-32767. |
| 5838 | 16 | No | The service broker connection authentication value is invalid. |
| 5839 | 16 | No | The service broker message forward store size cannot be set to 0. |
| 5840 | 16 | No | The service broker message forward mode is invalid. |
| 5841 | 16 | No | The default full-text language is not supported by the full-text search component. |
| 5842 | 16 | No | Too few worker threads are specified. The minimum is %d. |
| 5844 | 16 | No | User Instances are not supported in this edition of SQL Server. |
| 5846 | 16 | No | Common language runtime (CLR) execution is not supported under lightweight pooling. Disable one of two options: "clr enabled" or "lightweight pooling". |
| 5848 | 10 | Yes | Physical CPU id %u has been hot added to node id %u as logical CPU id %u. This is an informational message only. No user action is required. |
| 5849 | 10 | Yes | Online CPU addition is not supported in the current edition of SQL Server. |
| 5850 | 10 | Yes | Online addition of CPU resources cannot be completed. A software non-uniform memory access (soft-NUMA) configuration was specified at SQL Server startup that does not allow online addition of CPU resources. To use the additional CPU resources, either add the new CPUs to the soft-NUMA configuration and restart SQL Server, or remove the soft-NUMA configuration and restart SQL Server. |
| 5851 | 10 | No | The AccessCheckResult quota must be greater than or equal to the bucket count |
| 5852 | 10 | No | The AccessCheckResult bucket count must be less than %d. |
| 5853 | 16 | No | The affinity range is invalid. The lower bound %d must be less than the upper bound %d. |
| 5854 | 16 | No | A %S_MSG value was specified more than one time in the range list for an ALTER SERVER CONFIGURATION SET PROCESS AFFINITY statement. |
| 5855 | 16 | No | The affinity setting was not changed. This can be caused by low system resources. |
| 5856 | 16 | No | The %S_MSG range that specifies %S_MSG %d includes at least one %S_MSG that is not available to the current instance. The maximum %S_MSG number that is available to this instance is %d. |
| 5857 | 10 | No | CPU |
| 5858 | 10 | No | NUMANODE |
| 5859 | 16 | No | The current affinity setting specifies the use of more than 64 processors. Before you use sp_configure to change affinity settings, remove these processors by using ALTER SERVER CONFIGURATION. |
| 5860 | 10 | No | Affinity changed for node %d: from 0x%0\*I64x:%u to 0x%0\*I64x:%u. This is an informational message only. No user action is required. |
| 5861 | 16 | No | A %S_MSG with id %d does not exist on this system. Use sys.dm_os_schedulers to locate valid %S_MSGs for this system. |
| 5862 | 16 | No | The number of max worker threads is set too low. On this computer, the number must be more than %u. You should increase the number of max worker threads. |
| 5863 | 16 | No | Could not change the value of the '%.\*ls' property. Operating system error %ls |
| 5864 | 16 | No | IO affinity is not supported on this edition of sql server. |
| 5865 | 10 | No | Dynamic configuration setting %ls\%ls has been changed to %ld. |
| 5866 | 10 | No | Max server memory specified - %I64d MB is greater than the buffer pool extension size - %I64d MB. Buffer pool extension would be disabled on restart. |
| 5867 | 16 | No | Changing AFFINITY is not supported when the sql server is running in agnostic affinity mode. |
| 5868 | 16 | No | File system DMVs and DMFs have been disabled. |
| 5869 | 16 | No | Changes to server configuration option %s are not supported in SQL Database Managed Instances. |
| 5870 | 16 | No | Changes to server configuration option '%s' are not supported in this edition of SQL Server. |
| 5871 | 16 | No | Cannot set the column encryption enclave type to Virtualization-based security (VBS) - the operating system does not support VBS. |
| 5872 | 16 | No | Invalid column encryption enclave type %d specified. |
| 5873 | 16 | No | Cannot set the column encryption enclave type to Software Guard Extension (SGX)- the operating system does not support SGX. |
| 5874 | 16 | No | Changes to server configuration options are not permitted in the connection to Contained Availability Group. Change connection to SQL Server instance level and retry the operation. |
| 5901 | 16 | No | One or more recovery units belonging to database '%.\*ls' failed to generate a checkpoint. This is typically caused by lack of system resources such as disk or memory, or in some cases due to database corruption. Examine previous entries in the error log for more detailed information on this failure. |
| 5904 | 17 | Yes | Unable to issue checkpoint: there are not enough locks available. Background checkpoint process will remain suspended until locks are available. To free up locks, list transactions and their locks, and terminate transactions with the highest number of locks. |
