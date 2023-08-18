---
author: MashaMSFT
ms.author: mathoma
ms.reviewer: randolphwest
ms.date: 07/06/2023
ms.topic: include
---
| Error | Severity | Event logged | Description |
| :--- | :--- | :--- | :--- |
| 22001 | 16 | No | FreeStaleVersionSpace failed for page %S_PGID for database id '%d'. It will be retired in the next iteration of the version cleaner. |
| 22002 | 17 | No | Internal Error: A expected large object wasn't found. |
| 22003 | 16 | No | Stale/aborted version cleanup was aborted for database id '%d' due to database shutdown. |
| 22004 | 10 | No | \[%d\]. System transaction with xdes id %S_XID was aborted due to failure injection while moving rows from one page to another. |
| 22005 | 10 | No | ADR cleanup failed for database id '%d'. |
| 22006 | 16 | No | Version cleanup was aborted for database id '%d' due to database exclusive waiter. |
| 22007 | 16 | No | Version cleanup was aborted for database id '%d' due to planned failover. |
| 22008 | 16 | No | Aborted versions belonging to this filegroup could not be cleaned up. |
| 22010 | 16 | No | Cannot change the READONLY property of the filegroup containing Persistent Version Store which is required for Accelerated Database Recovery. |
| 22012 | 16 | No | Persistent version store is enabled on the database '%.\*ls' but the version store manager could not be initialized. |
| 22020 | 17 | No | Internal Error: Tried to access an expired large object. |
| 22101 | 16 | No | The value supplied for the change_columns argument of CHANGE_TRACKING_IS_COLUMN_IN_MASK function is not valid. The value must be a bitmask returned by the CHANGETABLE(CHANGES ...) function. |
| 22102 | 16 | No | The arguments supplied are not valid for the CHANGES option of the CHANGETABLE function. |
| 22103 | 16 | No | The arguments supplied are not valid for the VERSION option of the CHANGETABLE function. |
| 22104 | 16 | No | A table returned by the CHANGETABLE function must be aliased. |
| 22105 | 16 | No | Change tracking is not enabled on table '%.\*ls'. |
| 22106 | 16 | No | The CHANGETABLE function does not support remote data sources. |
| 22107 | 16 | No | Object '%.\*ls' is of a data type that is not supported by the CHANGETABLE function. The object must be a user-defined table. |
| 22108 | 16 | No | The CHANGE_TRACKING_CONTEXT WITH clause cannot be used with a SELECT statement. |
| 22109 | 16 | No | The "context" argument for the CHANGE_TRACKING_CONTEXT WITH clause must be of type varbinary data type with a maximum length of 128. |
| 22110 | 16 | No | The number of columns specified in the CHANGETABLE(VERSION ...) function does not match the number of primary key columns for table '%.\*ls'. |
| 22111 | 16 | No | The column '%.\*ls' specified in the CHANGETABLE(VERSION ...) function is not part of the primary key for table '%.\*ls'. |
| 22112 | 16 | No | Each primary key column must be specified once in the CHANGETABLE(VERSION ...) function. The column '%.\*ls' is specified more than once. |
| 22113 | 16 | No | %S_MSG is not allowed because the table is being tracked for change tracking. |
| 22114 | 16 | No | Change tracking options for ALTER DATABASE cannot be combined with other ALTER DATABASE options. |
| 22115 | 16 | No | Change tracking is enabled for one or more tables in database '%.\*ls'. Disable change tracking on each table before disabling it for the database. Use the sys.change_tracking_tables catalog view to obtain a list of tables for which change tracking is enabled. |
| 22116 | 16 | No | Change tracking is not supported by this edition of SQL Server. |
| 22117 | 16 | No | For databases that are members of a secondary availability replica, change tracking is not supported. Run change tracking queries on the databases in the primary availability replica. |
| 22118 | 16 | No | Cannot enable change tracking on table '%.\*ls'. Change tracking is not supported when the primary key contains encrypted columns. |
| 22119 | 16 | No | Cannot enable change tracking on table '%.\*ls'. Change tracking requires a primary key constraint on the table to be enabled. Enable the primary key constraint on the table before enabling change tracking. |
| 22120 | 16 | No | Invalid value for cleanup batch size. |
| 22121 | 16 | No | Deleted %ld row(s) per millisecond from %s |
| 22122 | 16 | No | Change Tracking autocleanup failed on side table of "%s". If the failure persists, use sp_flush_CT_internal_table_on_demand to clean up expired records from its side table. |
| 22123 | 16 | No | Change Tracking autocleanup is blocked on side table of "%s". If the failure persists, check if the table "%s" is blocked by any process . |
| 22124 | 16 | No | Change Tracking manual cleanup is blocked on side table of "%s". If the failure persists, check if the table "%s" is blocked by any process . |
| 22125 | 16 | No | Change tracking autocleanup is currently not able to maintain retention for database ID %d. Number of expired records: %d. If this warning persists, check the following resource: [https://learn.microsoft.com/sql/relational-databases/track-changes/cleanup-and-troubleshoot-change-tracking-sql-server](../../track-changes/cleanup-and-troubleshoot-change-tracking-sql-server.md) |
| 22201 | 16 | No | Internal error. Unable to acquire the latch holding buffers for DW Tiered Storage ColumnStore Scan. |
| 22202 | 16 | No | Internal error. Unable to run the remote cs garbage collector. Error Code 22202. |
| 22203 | 16 | No | Internal error. Unable to update the blobs table in the catalogDB. Error Code 22203. |
| 22204 | 16 | No | Internal error. Unable to refresh catalog db information for service uri \[%ls\]. |
| 22205 | 16 | No | Internal error. Unable to get catalog information via the catalog helper. |
| 22206 | 16 | No | Internal error. Unable to get lock for protected shared buffer |
| 22207 | 16 | No | Internal error. Unable to get a valid dbtable. Error Code 22207. |
| 22208 | 16 | No | Access to DW Tiered Storage ColumnStore blob failed. See earlier errors for cause. |
| 22209 | 16 | No | Internal error. Unable to populate instance member list. |
| 22210 | 16 | No | Internal error. Unable to get instance member. |
| 22211 | 16 | No | Internal error. Invalid instance member state. |
| 22212 | 21 | No | An error occurred while reading remote column store segment HoBt 0x%I64X, Object %d, Column %d, Type %d in database %d. The segement could not be decrypted. |
| 22213 | 16 | No | Internal error. Unable to get catalog information via the sp. |
| 22214 | 16 | No | Internal error. Unable to initialise XODBC Connection Manager. |
| 22215 | 16 | No | Internal error. Unable to get catalog information. |
| 22216 | 16 | No | Internal error. Protected buffer failure. |
| 22217 | 16 | No | Internal error. Persist lru cost info failure. |
| 22218 | 16 | No | Internal error. Catalog Communication Failure. |
| 22219 | 16 | No | Internal error. Internal table base failure. |
| 22220 | 10 | No | Beginning database migration scan for database "%s". |
| 22221 | 10 | No | Database migration scan for database "%s" is complete. |
| 22222 | 10 | No | Database migration scan for database '%.\*ls' was aborted. Internal error. Migration scan was aborted. |
| 22223 | 16 | No | Internal error. Unable to refresh migration type from fabric property. |
| 22224 | 16 | No | Internal error. ADW Optimized for Compute storage detected. Unable to retrieve blob. |
| 22225 | 16 | No | An internal error (%d, %d) occurred. Please retry the operation. If the problem persists contact Microsoft Azure Customer Support. |
| 22226 | 16 | No | An internal error (%d, %d) occurred. Please retry the operation. If the problem persists contact Microsoft Azure Customer Support. |
| 22227 | 10 | No | TIERED Storage Scanner encountered an error message "%ls" in "%ls". |
| 22228 | 22 | No | The columnstore remote lob header is invalid. |
| 22229 | 22 | No | Remote storage columnstore data checksum mismatch. Expected checksum from blob is %lu, actual check sum from read buffers is %lu. |
| 22301 | 16 | No | DW FIDO mode is not enabled. |
| 22302 | 16 | No | DW FIDO transaction context not found. |
| 22303 | 16 | No | Updates are not allowed from a FIDO Scan transaction. |
| 22304 | 16 | No | Reading or Writing to database files is not supported in FIDO DBs. |
| 22305 | 16 | No | A NULL or unexpected value was returned by an ODBC call. |
| 22306 | 16 | No | Only CCI tables are allowed in Fido mode. |
| 22307 | 16 | No | Alter statements are only allowed from a FIDO Alter transaction. |
| 22308 | 16 | No | Fido thread failed to acquire a lock. |
| 22309 | 16 | No | Fido Cache DB not found. |
| 22310 | 16 | No | Failed to create Fido DB with key: \[%.\*ls\]. |
| 22311 | 16 | No | Generic Fido out of bounds error. |
| 22312 | 16 | No | Failed to remap rowset with Id '%I64d' on a Fido DB. |
| 22313 | 16 | No | Failed to find Fido columns in rowset with Id '%I64d'. |
| 22314 | 16 | No | Fido invalid ODBC connection. |
| 22315 | 16 | No | Invalid Fido Transaction type %d. |
| 22316 | 16 | No | Failed to acquire CSI Cache lock. |
| 22317 | 16 | No | Fido invalid ODBC column. |
| 22318 | 16 | No | Fido ODBC transaction failed a commit. |
| 22319 | 16 | No | An invalid access to a Fido DB Rowset (DbId '%lu', RowsetId '%I64d') was performed. |
| 22320 | 16 | No | Fido DB (DbId:'%lu', Name: '%.\*ls') can only be used under a Fido session context. |
| 22321 | 16 | No | Fido DB (DbId:'%lu', Name: '%.\*ls') cannot be used in current session. Only DbId: '%lu' is allowed. |
| 22322 | 16 | No | Fido session context invalid. Min cell Id cannot greater than Max cell Id |
| 22323 | 16 | No | DW FIDO GLM server is not initialized. |
| 22324 | 16 | No | DW FIDO GLM Client is not initialized. |
| 22325 | 16 | No | The Key column Id (%d) for Rowset (%I64d) is out of range. |
| 22326 | 16 | No | Updates are not allowed from a Scan only FIDO Rowset. |
| 22327 | 16 | No | Invalid Rowset Id (%I64d) was provided to a Fido Rowset remapping sys RowsetId (%I64d). |
| 22328 | 16 | No | Alters are only allowed on the GLMServer instance. |
| 22329 | 16 | No | Open of Rowset (%I64d) in DB (%d) failed. |
| 22330 | 16 | No | RowsetColumn Id (%d) missing in Rowset (%I64d). |
| 22331 | 16 | No | Provided Accessor Mode is not supported in Fido GLM Rowset. |
| 22332 | 16 | No | Data unsupported by Fido GLM Rowset. |
| 22500 | 16 | No | Unexpected |
| 22501 | 16 | No | All articles in the publication passed data validation (rowcount and checksum). |
| 22502 | 16 | No | Not All articles in the publication passed data validation (rowcount only) |
| 22503 | 16 | No | Initializing. |
| 22504 | 16 | No | Applying the snapshot to the Subscriber. |
| 22505 | 16 | No | The merge completed with no data changes processed. |
| 22506 | 16 | No | No data needed to be merged. |
| 22507 | 16 | No | Uploading data changes to the Publisher. |
| 22508 | 16 | No | Downloading data changes to the Subscriber. |
| 22509 | 16 | No | Retrieving subscription information. |
| 22510 | 16 | No | Retrieving publication information. |
| 22511 | 16 | No | The merge completed successfully. |
| 22512 | 16 | No | Cannot use partition groups with unfiltered publications. Set "use_partition_groups" to "false" using sp_changemergepublication. |
| 22513 | 16 | No | Cannot use partition groups because the join filter between the following articles contains one or more functions: "%s" and "%s". |
| 22514 | 16 | No | Cannot use partition groups because one or more filters reference the following view, which contains functions: "%s". |
| 22515 | 16 | No | The publication cannot use precomputed partitions because there is at least one circular reference in the join filters specified for the articles in the publication. To use precomputed partitions, ensure that no circular join filter relationships exist. |
| 22516 | 16 | No | The publication "%s" was defined as having dynamic filters, but it does not contain any dynamic filters. |
| 22517 | 16 | No | The publication was defined as having no dynamic filters, but contains one or more dynamic filters. |
| 22518 | 16 | No | Cannot use column of type image, ntext, xml, CLR type, varchar(max), nvarchar(max), or varbinary(max) in a subset or join filter for article: '%s'. |
| 22519 | 16 | No | Cannot add a logical record relationship between tables "%s" and "%s" because a text, image, ntext, xml, varchar(max), nvarchar(max), or varbinary(max) column was referenced in the join clause. |
| 22520 | 10 | No | A filtering type changed for the article. Any pending or future changes made in this article by a Subscriber in a given partition will no longer be propagated to Subscribers in other partitions. Check the documentation for details. |
| 22521 | 10 | No | Unable to synchronize the row because the row was updated by a different process outside of replication. |
| 22522 | 16 | No | Article '%s' cannot be published because it is published in another merge publication. An article that has a value of 3 for the @partition_options parameter of sp_addmergearticle (nonoverlapping partitions with a single subscription per partition) cannot be included in multiple publications or subscriptions, and cannot be republished. To include the article in multiple publications, use sp_changemergearticle to specify a different value for the partition_options property of the existing article. |
| 22523 | 16 | No | An article cannot use @partition_options 2 or 3 (nonoverlapping partitions) and be a part of a logical record relationship at the same time. Check article "%s". |
| 22524 | 16 | No | Article '%s' is published in another merge publication, with a different value specified for the @partition_options parameter of sp_addmergearticle. The specified value must be the same in all merge publications. Either specify the same value as the existing article or change the existing article using sp_changemergearticle. |
| 22525 | 16 | No | The publication "%s" cannot allow multiple subscriptions per partition if it contains articles using @partition_options = 3. |
| 22526 | 16 | No | An invalid value was specified for %s. Valid values are 0 (none), 1 (enforced partitions), 2 (nonoverlapping partitions with multiple subscriptions per partition), and 3 (nonoverlapping partitions with single subscription per partition). |
| 22527 | 16 | No | Invalid value specified for %s. Valid values are 'day', 'days', 'dd', 'year', 'years', 'yy', 'yyyy', 'month', 'months', 'mm', 'week', 'weeks', 'wk', 'hour', 'hours', 'hh', 'minute', 'minutes', 'mi'. |
| 22528 | 16 | No | Cannot use a retention period unit other than "days" for publication "%s" because the compatibility level of the publication is lower than 90. Use sp_changemergepublication to set publication_compatibility_level to 90RTM. |
| 22529 | 16 | No | Cannot change the retention period unit for publication "%s" because the compatibility level of the publication is lower than 90. Use sp_changemergepublication to set publication_compatibility_level to 90RTM. |
| 22530 | 16 | No | Cannot update any column in article "%s" that is used in a logical record relationship clause. |
| 22531 | 10 | No | Initialization. |
| 22532 | 10 | No | Upload of Subscriber changes to the Publisher. |
| 22533 | 10 | No | Download of Publisher changes to the Subscriber. |
| 22534 | 16 | No | Character mode publication does not support partitioned tables. |
| 22535 | 16 | No | For heterogeneous publications, the %s parameters should be specified when calling "%s". |
| 22536 | 16 | No | The %s parameter value cannot be updated or changed for heterogeneous publications. |
| 22537 | 16 | No | The job_login provided must match the Publisher login specified when adding the distribution Publisher (sp_adddistpublisher). |
| 22538 | 16 | No | Only replication jobs or job schedules can be added, modified, dropped or viewed through replication stored procedures. |
| 22539 | 16 | No | Use of parameters %s is invalid when parameter %s is set to %s. |
| 22540 | 16 | No | Cannot change publication "%s" to use sync_mode of "character", because it contains one or more logical record relationships. |
| 22541 | 16 | No | Cannot add a logical record relationship in publication "%s" because it uses sync_mode of "character" and could have SQL Server Compact Edition subscribers. |
| 22542 | 16 | No | Invalid value for property @subscriber_upload_options. Valid values are 0 (allow uploads), 1 (disable uploads), 2 (disable uploads prohibit subscriber changes), and 3 (disable_outofpartition_subscriber_changes). |
| 22543 | 16 | No | When the publication property @allow_partition_realignment is set to "false", the article property @subscriber_upload_options for all articles in the publication must be set to disable uploads. |
| 22544 | 10 | No | Warning: The procedure sp_mergecleanupmetadata has been deprecated. In SQL Server 2000 SP1 and later, the merge agent calls sp_mergemetadataretentioncleanup every time it runs, so manual cleanup of metadata is not needed. Ignoring passed-in parameters and calling sp_mergemetadataretentioncleanup. |
| 22545 | 16 | No | Cannot add a logical record relationship in publication "%s" because it allows Web synchronization. |
| 22546 | 16 | No | Cannot change publication "%s" to allow Web synchronization because it contains one or more logical record relationships. |
| 22547 | 16 | No | A concurrent snapshot is not allowed for snapshot publications. |
| 22548 | 16 | No | Vertical partitioning is only allowed for log-based articles. |
| 22549 | 16 | No | A shared distribution agent (%s) already exists for this subscription. |
| 22550 | 16 | No | Cannot drop identity column "%s" from the vertical partition when identityrangemanagementoption is set to auto. |
| 22551 | 16 | No | The type "%s" is invalid. Valid types are "merge", "tran", and "both". |
| 22552 | 16 | No | A valid value for parameter "@resync_date_str" needs to be provided when "@resync_type" is set to 2. |
| 22553 | 16 | No | The parameter "@resync_type" is set to "%d" but this subscription has never been successfully validated. |
| 22554 | 16 | No | Cannot change publication "%s" to use the sync_mode of "character" because it uses a retention period unit other than "day". Use sp_changemergepublication to set the retention period unit to "day". |
| 22555 | 16 | No | Cannot set the retention period unit to a value other than "day" for publication "%s" because it uses the sync_mode of "character" and may have SQL Server Compact Edition subscribers. |
| 22556 | 16 | No | Invalid value for the property "%s". Valid values are 1 and 0. |
| 22557 | 16 | No | The status of the schema change could not be updated because the publication compatibility level is less than 90. Use sp_changemergepublication to set the publication_compatibility_level of publication "%s" to 90RTM. |
| 22558 | 16 | No | The status of the schema change could not be updated. |
| 22559 | 16 | No | The status of the schema change must be "active" or "skipped". |
| 22560 | 16 | No | Merge replication does not allow filters that reference dynamic functions that take one or more parameters. Check the function "%s". |
| 22561 | 16 | No | The requested operation failed because the publication compatibility level is less than 90. Use sp_changemergepublication to set the publication_compatibility_level of publication "%s" to 90RTM. |
| 22562 | 16 | No | Cannot change the compatibility level of a publication to a value lower than the existing value. |
| 22563 | 16 | No | contains one or more articles that do not upload changes |
| 22564 | 16 | No | uses ddl replication |
| 22565 | 16 | No | uses other than day as unit of retention period |
| 22566 | 16 | No | uses logical records |
| 22567 | 16 | No | contains one or more articles that use subscription-based or partition-based filtering |
| 22568 | 16 | No | contains one or more articles which will not compensate for errors |
| 22569 | 16 | No | contains one or more schema only articles |
| 22570 | 16 | No | contains one or more articles that use automatic identity range management |
| 22571 | 16 | No | contains one or more articles that use datatypes new in SQL Server 2000 |
| 22572 | 16 | No | contains one or more articles with a timestamp column |
| 22573 | 16 | No | uses snapshot compression with snapshot_in_defaultfolder set to false |
| 22574 | 16 | No | contains one or more articles that use vertical partitioning |
| 22575 | 16 | No | When article property 'published_in_tran_pub' is set to 'true' then article property 'upload_options' has to be set to disable uploads. |
| 22576 | 10 | No | Invalid failover_mode value of %d was specified for \[%s\].\[%s\].\[%s\], setting to 0 \[immediate\]. |
| 22578 | 16 | No | Cannot change publication "%s" to disallow use_partition_groups because it contains one or more logical record relationships. When using logical record relationships the publication must set the @use_partition_groups property to 'true'. |
| 22579 | 16 | No | The subscription to publication '%s' was not found but a shared agent does exist. To specify a subscription to a publication that is replicated via a shared agent specify '%s' for the publication name. |
| 22580 | 16 | No | Cannot publish database '%s' because it is marked as published on a different server. Before attempting to publish this database, execute sp_replicationdboption, specifying a value of FALSE for 'publish' and 'merge publish'. |
| 22581 | 16 | No | Article '%s' cannot be added or modified in publication '%s'. The replication of FILESTREAM columns is not supported for publications that have a 'sync_mode' of 1 (character mode). Specify a 'sync_mode' of 0 (native mode) for the publication by using sp_addmergepublication or sp_changemergepublication, or partition the article vertically so that the FILESTREAM column is not replicated. |
| 22582 | 16 | No | Article '%s' cannot be added or modified in publication '%s'. The replication of FILESTREAM columns is not supported for publications that have a 'publication_compatibility_level' of less than "90RTM" (SQL Server 2005). Specify a 'publication_compatibility_level' greater than or equal to "90RTM" by using sp_addmergepublication or sp_changemergepublication, or partition the article vertically so that the FILESTREAM column is not replicated. |
| 22583 | 16 | No | Article '%s' cannot be added or modified in publication '%s'. The replication of FILESTREAM columns is not supported for articles that have a 'schema_option' set to 0x20000000. This converts large object data types to data types that are supported on earlier versions of Microsoft SQL Server. Remove this 'schema_option' setting by using sp_addmergepublication or sp_changemergepublication, or partition the article vertically so that the FILESTREAM column is not replicated. |
| 22584 | 10 | No | Warning: Values of some of the flags specified in the 'schema_option' property are not compatible with the publication's compatibility level. The modified schema_option value of '%s' will be used instead. |
| 22585 | 10 | No | The schema option to script out the FILESTREAM attribute on varbinary(max) columns has been enabled for article '%s'. Enabling this option after the article is created can cause replication to fail when the data in a FILESTREAM column exceeds 2GB and there is a conflict during replication. If you want FILESTREAM data to be replicated, drop and re-create the article, and specify the appropriate schema option when you re-create the article. |
| 22586 | 16 | No | Column '%s' cannot be added or modified in article '%s' of publication '%s'. The DDL operatoin on hierarchyid and FILESTREAM columns is not supported for publications that have a 'sync_mode' of 1 (character mode) or with a lower than 90RTM backward compatibility level. |
| 22587 | 16 | No | Non-SQL Server Publishers and Subscribers are supported only on Windows. The platform detected is %s. |
| 22588 | 16 | No | Publications on non-Windows platforms cannot support updateable subscriptions. The platform detected is %s. The values of @allow_sync_tran and @allow_queued_tran must be 'false' or NULL. |
| 22801 | 16 | No | Starting the Change Data Capture Collection Agent job. To report on the progress of the operation, query the sys.dm_cdc_log_scan_sessions dynamic management view. |
| 22802 | 16 | No | Starting the Change Data Capture Cleanup Agent job using low watermark %s. |
| 22803 | 16 | No | Change Data Capture has scanned the log from LSN{%s} to LSN{%s}, %d transactions with %d commands have been extracted. To report on the progress of the operation, query the sys.dm_cdc_log_scan_sessions dynamic management view. |
| 22804 | 16 | No | Change Data Capture cannot proceed with the job-related action because transactional replication is enabled on database %s but Distributor information cannot be retrieved to determine the state of the logreader agent. Make the Distributor database available, or disable distribution. |
| 22805 | 10 | No | For more information, query the sys.dm_cdc_errors dynamic management view. |
| 22806 | 16 | No | The originator ID '%s' is not valid. You must specify a non-zero ID that has never been used in the topology. |
| 22807 | 16 | No | The publication property '%s' cannot be modified because the peer-to-peer publication '%s' is not enabled for conflict detection. To enable the publication for conflict detection, use sp_configure_peerconflictdetection. |
| 22808 | 16 | No | Cannot execute procedure '%s'. Publication '%s' must be enabled for peer-to-peer replication before you execute this procedure. To enable the publication for peer-to-peer replication, use sp_changepublication. |
| 22809 | 10 | No | The existing conflict table '%s' was dropped. |
| 22810 | 16 | No | The @action parameter value is not valid. Valid values are 'enable' and 'disable'. |
| 22811 | 16 | No | The roundtrip time-out must be greater than 0. |
| 22812 | 10 | No | The roundtrip '%s' finished with timeout: %d seconds. |
| 22813 | 10 | No | The topology contains peer node versions that do not support conflict detection. To use conflict detection, ensure that all nodes in the topology are SQL Server 2008 or later versions. |
| 22814 | 10 | No | The topology contains a duplicate originator ID. To use conflict detection, the originator ID must be unique across the topology. |
| 22815 | 10 | No | A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s and peer %d (on disk), transaction id %s for Table '%s' with Primary Key(s): %s Current Version '%s', Pre-Version '%s' and Post-Version '%s' |
| 22816 | 16 | No | The qualified table name '%s' is too long to be enabled for peer-to-peer conflict detection. |
| 22817 | 10 | No | %s has %s. |
| 22818 | 10 | No | A delete-delete conflict was detected and resolved. The row could not be deleted from the peer since the row does not exist. The incoming delete was skipped. |
| 22819 | 10 | No | A delete-update conflict between peer %d (incoming) and peer %d (on disk) was detected and could not be resolved automatically. The incoming delete was skipped by peer %d. The conflict has to be resolved manually to guarantee data convergence between the peers. For steps on how to resolve the conflict refer to BOL. |
| 22820 | 10 | No | A delete-update conflict between peer %d (incoming) and peer %d (on disk) was detected and resolved. The incoming delete was applied to peer %d. |
| 22821 | 10 | No | An update-update conflict between peer %d (incoming) and peer %d (on disk) was detected and resolved. The incoming update was skipped by peer %d. |
| 22822 | 10 | No | An update-update conflict between peer %d (incoming) and peer %d (on disk) was detected and resolved. The incoming update was applied to peer %d. |
| 22823 | 10 | No | An update-delete conflict was detected and unresolved. The row could not be updated since the row does not exist. The incoming update was skipped. Check the priority of the destination peer and run data validation to ensure the delete conflict did not result in data non-convergence. |
| 22824 | 10 | No | An insert-insert conflict between peer %d (incoming) and peer %d (on disk) was detected and resolved. The incoming insert was skipped by peer %d. |
| 22825 | 10 | No | An insert-insert conflict between peer %d (incoming) and peer %d (on disk) was detected and resolved. The incoming insert was applied to peer %d. |
| 22827 | 16 | No | Peer-to-peer conflict detection alert |
| 22828 | 16 | No | The publication '%s' was already %s for peer-to-peer conflict detection. |
| 22829 | 16 | No | The command %s failed. The values specified for the @ins_cmd, @del_cmd or @upd_cmd cannot be appended with schema name %s within the size limit %d. |
| 22830 | 16 | No | Could not update the metadata that indicates database %s is enabled for Change Data Capture. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22831 | 16 | No | Could not update the metadata that indicates database %s is not enabled for Change Data Capture. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22832 | 16 | No | Could not update the metadata that indicates table %s is enabled for Change Data Capture. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22833 | 16 | No | Could not update the metadata that indicates table %s is not enabled for Change Data Capture. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22834 | 16 | No | Could not modify the the verbose logging status for table %s. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22835 | 16 | No | Could not update the metadata for database %s to indicate that a Change Data Capture job has been dropped. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22836 | 16 | No | Could not update the metadata for database %s to indicate that a Change Data Capture job has been added. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22837 | 16 | No | Could not delete table entries or drop objects associated with capture instance '%s'. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22838 | 16 | No | All columns of a CDC unique index must be defined as NOT NULL. Index '%s' selected as the CDC unique index for source table '%s.%s' does not meet this requirement. Define all columns of the selected index as NOT NULL or select another unique index as the CDC index and resubmit the request. |
| 22840 | 16 | No | The application lock request '%s' needed to modify Change Data Capture metadata was not granted. The value returned from the request was %d: -1 = timeout; -2 = canceled; -3 = deadlock victim; -999 validation or other call error. Examine the error cause and resubmit the request. |
| 22841 | 16 | No | Could not upgrade the metadata for database '%s' that is enabled for Change Data Capture. The failure occurred when executing the action '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22842 | 16 | No | ALTER TABLE SWITCH statement failed because the partitioned destination table is enabled for Change Data Capture and does not have @allow_partition_switch set to 1. |
| 22843 | 16 | No | ALTER TABLE SWITCH statement failed because the partitioned source table is enabled for Change Data Capture and does not have @allow_partition_switch set to 1. |
| 22844 | 16 | No | The '%s' option must be either 1 or 0. |
| 22845 | 16 | No | Cannot enable change data capture in this edition of SQL Server. |
| 22850 | 16 | No | The threshold value specified for the Change Data Capture cleanup process must be greater than 0. When creating or modifying the cleanup job, specify a positive threshold value. If this error is encountered when executing the sys.sp_cdc_cleanup_change_table stored procedure, reset the threshold value associated with the job to a non-negative value by using the sp_cdc_change_job stored procedure. |
| 22851 | 16 | No | Could not update cdc.change_tables to indicate a change in the low water mark for database %s. |
| 22852 | 10 | No | Could not delete change table entries made obsolete by a change in one or more low water marks for capture instances of database %s. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22853 | 10 | No | Could not delete obsolete entries in the cdc.lsn_time_mapping table for database %s. The failure occurred when executing the command '%s'. The error returned was %d: '%s'. Use the action and error to determine the cause of the failure and resubmit the request. |
| 22854 | 16 | No | Can not enable Change Data Capture on table '%s' or add ColumnSet column to it because CDC does not support ColumnSet. |
| 22855 | 10 | No | Warning: The @allow_partition_switch parameter is set to 1. Change data capture will not track changes introduced in the table resulting from a partition switch which will cause data inconsistency when changes are consumed. Refer to books online for more information about partition switching behavior when using Change Data Capture. |
| 22856 | 10 | No | Warning: The @allow_partition_switch parameter is set to 0. ALTER TABLE ... SWITCH PARTITION statement will be disallowed on this partitioned table. Refer to books online for more information about partition switching behavior when using Change Data Capture. |
| 22857 | 10 | No | Warning: The @allow_partition_switch parameter must be 1 for tables that are not partitioned. The explicit setting of the parameter to 0 was ignored. Refer to books online for more information about partition switching behavior when using Change Data Capture. |
| 22858 | 16 | No | Unable to add entries to the Change Data Capture LSN time mapping table to reflect dml changes applied to the tracked tables. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22859 | 16 | No | Log Scan process failed in processing log records. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22860 | 16 | No | Log scan process failed in processing a ddl log record. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22861 | 10 | No | Unable to upgrade database '%s'. Error '%d' was raised: '%s'. Use the reported error to determine the cause of the failure and then execute sys.sp_cdc_vupgrade in the database context to rerun upgrade. |
| 22862 | 16 | No | The database snapshot '%s' does not exist. Correct the parameter value and resubmit the request. |
| 22863 | 16 | No | Failed to insert rows into Change Data Capture change tables. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22864 | 16 | No | The call to sp_MScdc_capture_job by the Capture Job for database '%s' failed. Look at previous errors for the cause of the failure. |
| 22865 | 16 | No | The number of columns in the index '%s', used as the unique row identifier to support net changes for table '%s'.'%s', exceeds the limit of 14 columns. Set the parameter @supports_net_changes to 0 or use the @index_name parameter to identify a unique index with fewer than 15 columns as the unique row identifier and resubmit the request. |
| 22866 | 10 | No | The value returned by %S_MSG is %I64d. |
| 22867 | 10 | No | Total rows deleted: %I64u. |
| 22868 | 10 | No | Cleanup Watermark = %I64u |
| 22869 | 10 | No | Internal Change Tracking table name : %s |
| 22870 | 10 | No | Deleted %I64u rows from %s |
| 22878 | 16 | No | The @p2p_conflictdetection_policy parameter value is not valid. Valid values are 'originatorid' and 'lastwriter'. |
| 22879 | 16 | No | Peer-to-peer publications with last writer conflict detection policy only supports CALL or SCALL command type for @upd_cmd. Change the value for parameter '@upd_cmd'. |
| 22880 | 16 | No | An insert-insert conflict between peer %d (incoming) with commit datetime value of '%s' and peer %d (on disk) with commit datetime value of '%s' was detected and resolved. The incoming insert was applied to peer %d. |
| 22881 | 16 | No | A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s, commit datetime '%s' and peer %d (on disk), transaction id %s, commit datetime '%s' for Table '%s' with Primary Key(s): %s Current Version '%s', Pre-Version '%s' and Post-Version '%s' |
| 22882 | 10 | No | An update-update conflict between peer %d (incoming) with commit dateime value of '%s' and peer %d (on disk) with commit datetime value of '%s' was detected and resolved. The incoming update was skipped by peer %d. |
| 22883 | 10 | No | An update-update conflict between peer %d (incoming) with commit datetime value of '%s' and peer %d (on disk) with commit datetime value of '%s' was detected and resolved. The incoming update was applied to peer %d. |
| 22884 | 10 | No | An delete-update conflict between peer %d (incoming) with commit datetime value of '%s' and peer %d (on disk) with commit datetime value of '%s'was detected and resolved. The incoming delete was skipped by peer %d. |
| 22885 | 16 | No | An insert-insert conflict between peer %d (incoming) with commit datetime value of '%s' and peer %d (on disk) with commit datetime value of '%s' was detected and resolved. The incoming insert was skipped by peer %d. |
| 22886 | 10 | No | An update-delete conflict was detected. The row could not be updated since the row does not exist. The incoming update was skipped. |
| 22889 | 10 | No | Warning: Unable to get database version for the subscription database '%s'. The sp_replmonitorsubscriptionpendingcmds may report incorrect number of pending commands for P2P replication. |
| 22891 | 16 | No | Could not enable '%S_MSG' for database '%s'. '%S_MSG' cannot be enabled on a DB with delayed durability set. |
| 22892 | 16 | No | Could not enable delayed durability on DB. Delayed durability cannot be enabled on a DB while '%S_MSG' is enabled. |
| 22901 | 16 | No | The database '%s' is not enabled for Change Data Capture. Ensure that the correct database context is set and retry the operation. To report on the databases enabled for Change Data Capture, query the is_cdc_enabled column in the sys.databases catalog view. |
| 22902 | 16 | No | Caller is not authorized to initiate the requested action. Sysadmin privileges are required. |
| 22903 | 16 | No | Another connection with session ID %I64d is already running 'sp_replcmds' for Change Data Capture in the current database. |
| 22904 | 16 | No | Caller is not authorized to initiate the requested action. DBO privileges are required. |
| 22905 | 10 | No | Database '%s' is already enabled for Change Data Capture. Ensure that the correct database context is set, and retry the operation. To report on the databases enabled for Change Data Capture, query the is_cdc_enabled column in the sys.databases catalog view. |
| 22906 | 16 | No | The database '%s' cannot be enabled for Change Data Capture because a database user named 'cdc' or a schema named 'cdc' already exists in the current database. These objects are required exclusively by Change Data Capture. Drop or rename the user or schema and retry the operation. |
| 22907 | 16 | No | Parameter @role_name cannot be empty. Specify a value for @role_name and retry the operation. Supply null as the value if no role is to be used to gate access to captured change data. |
| 22908 | 16 | No | Could not create the Change Data Capture objects in database '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22909 | 16 | No | Failed to cleanup the cdc.lsn_time_mapping table in database '%s' when the last database table enabled for Change Data Capture was disabled. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22910 | 16 | No | The cleanup request for database '%s' failed. The database is not enabled for Change Data Capture. |
| 22911 | 16 | No | The capture job cannot be used by Change Data Capture to extract changes from the log when transactional replication is also enabled on the same database. When Change Data Capture and transactional replication are both enabled on a database, use the logreader agent to extract the log changes. |
| 22913 | 16 | No | Could not drop the Change Data Capture objects in database '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22914 | 16 | No | Only members of the sysadmin or db_owner or db_ddladmin roles can perform this operation when Change Data Capture is enabled for a database. |
| 22916 | 16 | No | Could not grant SELECT permission for the change enumeration functions for capture instance '%s' and source table '%s.%s' for the specified role. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22918 | 16 | No | One or more columns in the list of included columns was not a captured column of the change table %s. |
| 22919 | 16 | No | One or more columns in the list of columns needing update flags was not a captured column of the change table %s. |
| 22920 | 16 | No | The named capture instance %s does not exist for database %s. |
| 22921 | 16 | No | Unable to generate scripts for all capture instances that the caller is authorized to access. To generate all such scripts, the parameters @column_list and @update_flag_list must both be null or empty.' |
| 22923 | 16 | No | Could not compute the new low endpoint for database '%s' from retention %d. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22924 | 16 | No | Could not clean up change tables for database '%s'. A failure occurred when attempting to clean up the database change tables based upon the current retention time. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22925 | 16 | No | The number of columns captured by capture instance '%s' exceeds the maximum allowed number: %d. Use the @captured_columns_list parameter to specify a subset of the columns less than or equal to the maximum allowed and resubmit the request. |
| 22926 | 16 | No | Could not create a capture instance because the capture instance name '%s' already exists in the current database. Specify an explicit unique name for the parameter @capture_instance. |
| 22927 | 16 | No | Capture instance name '%s' exceeds the length limit of 100 characters. Specify a name that satisfies the length constraint. |
| 22928 | 16 | No | Index name '%s' is not an index for table '%s.%s'. Specify a valid index name for the table. |
| 22929 | 16 | No | Index '%s' must be either a primary key or a unique index for table '%s.%s'. Specify an index that meets at least one of these requirements. |
| 22930 | 16 | No | Could not locate '%s' as a column of source table '%s.%s'. Specify a valid column name. |
| 22931 | 16 | No | Source table '%s.%s' does not exist in the current database. Ensure that the correct database context is set. Specify a valid schema and table name for the database. |
| 22932 | 16 | No | Capture instance name '%s' is invalid. Specify a valid name. See the topic 'Identifiers' in SQL Server Books Online for object name rules. |
| 22938 | 16 | No | Role name '%s' is invalid. Specify a valid name. See the topic 'Identifiers' in SQL Server Books Online for object name rules. |
| 22939 | 16 | No | The parameter @supports_net_changes is set to 1, but the source table does not have a primary key defined and no alternate unique index has been specified. |
| 22940 | 16 | No | Could not remove DDL history entries in the Change Data Capture metadata for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22941 | 16 | No | Could not retrieve column information for index '%s' of source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22942 | 16 | No | Columns specified in the captured column list could not be mapped to columns in source table '%s.%s'. Verify that the columns specified in the parameter @captured_column_list are delimited properly and match columns in the source table. |
| 22943 | 16 | No | Columns used to uniquely identify a row for net change tracking must be included in the list of captured columns. Add either the primary key columns of the source table, or the columns defined for the index specified in the parameter @index_name to the list of captured columns and retry the operation. |
| 22944 | 16 | No | Could not create the specified database role '%s' for gating access to change table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22945 | 16 | No | Could not add column information to the cdc.index_columns system table for the specified index for source table '%s.%s. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22946 | 16 | No | Could not add column information to the cdc.captured_columns system table for source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22947 | 16 | No | Could not create the change table for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22948 | 16 | No | Could not create the change enumeration functions for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22949 | 16 | No | Could not update the Change Data Capture metadata for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22950 | 16 | No | Could not remove index column entries in the Change Data Capture metadata for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22951 | 16 | No | Could not remove captured column entries in the Change Data Capture metadata for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22952 | 16 | No | Could not drop Change Data Capture objects created for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22953 | 16 | No | Could not remove Change Data Capture metadata for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22954 | 16 | No | Could not cleanup change tables for capture instance '%s' using low end point %s. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22955 | 16 | No | Could not obtain the maximum LSN for the database from function 'sys.fn_cdc_get_max_lsn'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22956 | 16 | No | Could not obtain the minimum LSN of the change table associated with capture instance '%s' from function 'sys.fn_cdc_get_min_lsn'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22957 | 16 | No | LSN %s, specified as the new low end point for the change table associated with capture instance '%s', is not within the Change Data Capture timeline \[%s, %s\]. |
| 22958 | 16 | No | Could not create the function to query for all changes for capture instance '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22959 | 16 | No | Could not create the function to query for net changes for capture instance '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22960 | 16 | No | Change data capture instance '%s' has not been enabled for the source table '%s.%s'. Use sys.sp_cdc_help_change_data_capture to verify the capture instance name and retry the operation. |
| 22961 | 16 | No | Could not create a nonclustered index to support net change tracking for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22962 | 16 | No | Two capture instances already exist for source table '%s.%s'. A table can have at most two capture instances. If the current tracking options are not appropriate, disable change tracking for the obsolete instance by using sys.sp_cdc_disable_table and retry the operation. |
| 22963 | 16 | No | Parameter '%s' cannot be null or empty. Specify a value for the named parameter and retry the operation. |
| 22964 | 16 | No | LSN %s, specified as the new low end point for change table cleanup must represent the start_lsn value of a current entry in the cdc.lsn_time_mapping table. Choose an LSN value that satisfies this requirement. |
| 22965 | 16 | No | A quoted column in the column list is not properly terminated. Verify that columns are correctly delimited and retry the operation. For more information, see 'Delimited Identifiers' in Books Online. |
| 22966 | 16 | No | Could not create table dbo.systranschemas in database '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22967 | 16 | No | Could not create a clustered index for table dbo.systranschemas in database '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22968 | 16 | No | Could not create DDL trigger '%s' when enabling Change Data Capture for database '%s'. Additional messages in the SQL Server error log and operating system error log may provide more detail. |
| 22970 | 16 | No | The value for parameter @maxscans specified for the Change Data Capture job must be greater than 0. |
| 22971 | 16 | No | Could not allocate memory for the log reader history cache. Verify that SQL Server has sufficient memory for all operations. Check the physical and virtual settings on the server and examine memory usage to see if another application is excessively consuming memory. |
| 22972 | 16 | No | When calling stored procedure \[sys\].sp_cdc_help_change_data capture, if either @source_schema or @source_name is non-null and non-empty, the other parameter must also be non-null and non-empty. |
| 22973 | 16 | No | The specified filegroup '%s' is not a valid filegroup for database '%s'. Specify a valid existing filegroup or create the named filegroup, and retry the operation. |
| 22974 | 16 | No | Tables contained in the cdc schema cannot be enabled for Change Data Capture. |
| 22975 | 16 | No | Source table '%s' contains one of the following reserved column names: __$start_lsn, __$end_lsn, __$seqval, __$operation, and __$update_mask. To enable Change Data Capture for this table, specify a captured column list and ensure that these columns are excluded from the list. |
| 22976 | 16 | No | Could not alter column '%s' of change table '%s' in response to a data type change in the corresponding column of the source table '%s'. The Change Data Capture meta data for source table '%s' no longer accurately reflects the source table. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22977 | 16 | No | Unable to update DDL history information to reflect columns changes applied to the tracked table associated with change table '%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22978 | 16 | No | Could not update the cdc.captured_columns entry for column '%s' of change table '%s' to reflect a data type change in the corresponding column of the source table '%s'. Change Data Capture column meta data for table '%s' no longer accurately reflects the source table. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22979 | 16 | No | The unique index '%s' on table '%s' is used by Change Data Capture. The constraint using this index cannot be dropped or disabled. |
| 22980 | 16 | No | The unique index '%s' on table '%s.%s' is disabled and cannot be used as a unique index by Change Data Capture. Enable the index. |
| 22981 | 16 | No | Object does not exist or access is denied. |
| 22982 | 16 | No | Could not create internal stored procedures used to populate the change table for capture instance '%s' and source table '%s.%s'. Refer to previous errors in the current session to identify the cause and correct any associated problems. |
| 22983 | 16 | No | The unique index '%s' on source table '%s' is used by Change Data Capture. To alter or drop the index, you must first disable Change Data Capture on the table. |
| 22984 | 16 | No | An error occurred while waiting on the log reader history cache event. This error is reported by the internal task scheduling and might be transient. Retry the operation. |
| 22985 | 16 | No | Change data capture has not been enabled for source table '%s.%s'. Specify the name of a table enabled for Change Data Capture. To report on the tables enabled for Change Data Capture, query the is_tracked_by_cdc column in the sys.tables catalog view. |
| 22986 | 16 | No | Could not allocate memory for Change Data Capture population. Verify that SQL Server has sufficient memory for all operations. Check the physical and virtual memory settings on the server and examine memory usage to see if another application is consuming excessive memory. |
| 22987 | 16 | No | Change Data Capture population failed writing blob data for one or more large object columns. Verify that SQL Server has sufficient memory for all operations. Check the physical and virtual memory settings on the server and examine memory usage to see if another application is consuming excessive memory. |
| 22988 | 16 | No | This instance of SQL Server is the %s. Change data capture is only available in the Enterprise, Developer, Enterprise Evaluation, and Standard editions. |
| 22989 | 16 | No | Could not enable Change Data Capture for database '%s'. Change data capture is not supported on system databases, or on a distribution database. |
| 22990 | 16 | No | The value specified for the parameter @pollinginterval cannot exceed 24 hours or be less than 0. Specify a polling interval (in seconds) that is less than or equal to 24 hours (86,400 seconds). |
| 22991 | 16 | No | The value specified for the parameter @maxtrans must be greater than 0. |
| 22992 | 16 | No | The specified @job_type, %s, is not supported. The value specified for the parameter @job_type must be N'capture' to indicate a capture job, or N'cleanup' to indicate a cleanup job. |
| 22993 | 16 | No | The Change Data Capture job table containing job information for database '%s' cannot be found in the msdb system database. Run the stored procedure 'sys.sp_cdc_add_job' to create the appropriate CDC capture or cleanup job. The stored procedure will create the required job table. |
| 22994 | 16 | No | The retention value specified for the Change Data Capture cleanup process must be greater than 0 and less than or equal to 52594800. When creating or modifying the cleanup job, specify a retention value (in minutes) that is within that range. If this error is encountered when executing the sys.sp_cdc_cleanup_change_table stored procedure, reset the retention value associated with the job to a non-negative value less than 52594800 by using the sp_cdc_change_job stored procedure. |
| 22995 | 16 | No | A value for the parameter @retention cannot be specified when the job type is 'capture'. Specify NULL for the parameter, or omit the parameter from the statement. |
| 22996 | 16 | No | When adding or modifying the CDC cleanup job, @pollinginterval, @maxtrans, @maxscans, and @continuous may not be assigned non-null values. |
| 22997 | 16 | No | The Change Data Capture '%s' job does not exist in the system table 'msdb.dbo.cdc_jobs'. Use the stored procedure 'sys.sp_cdc_add_job' to add the Change Data Capture job. |
| 22998 | 16 | No | The value specified for the parameter @continuous must be 0 or 1. |
| 22999 | 16 | No | The value specified for the parameter @pollinginterval must be null or 0 when the stored procedure 'sys.sp_cdc_scan' is not being run in continuous mode. |
