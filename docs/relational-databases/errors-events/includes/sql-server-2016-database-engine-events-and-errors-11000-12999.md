---
author: MashaMSFT
ms.author: mathoma
ms.reviewer: randolphwest
ms.date: 07/06/2023
ms.topic: include
---
| Error | Severity | Event logged | Description |
| :--- | :--- | :--- | :--- |
| 11000 | 16 | No | Unknown status code for this column. |
| [11001](../mssqlserver-11001-database-engine-error.md) | 16 | No | Non-NULL value successfully returned. |
| 11002 | 16 | No | Deferred accessor validation occurred. Invalid binding for this column. |
| 11003 | 16 | No | Could not convert the data value due to reasons other than sign mismatch or overflow. |
| 11004 | 16 | No | Successfully returned a NULL value. |
| 11005 | 16 | No | Successfully returned a truncated value. |
| 11006 | 16 | No | Could not convert the data type because of a sign mismatch. |
| 11007 | 16 | No | Conversion failed because the data value overflowed the data type used by the provider. |
| 11008 | 16 | No | The provider cannot allocate memory or open another storage object on this column. |
| 11009 | 16 | No | The provider cannot determine the value for this column. |
| 11010 | 16 | No | The user did not have permission to write to the column. |
| 11011 | 16 | No | The data value violated the integrity constraints for the column. |
| 11012 | 16 | No | The data value violated the schema for the column. |
| 11013 | 16 | No | The column had a bad status. |
| 11014 | 16 | No | The column used the default value. |
| 11015 | 16 | No | The column was skipped when setting data. |
| 11031 | 16 | No | The row was successfully deleted. |
| 11032 | 16 | No | The table was in immediate-update mode, and deleting a single row caused more than one row to be deleted in the data source. |
| 11033 | 16 | No | The row was released even though it had a pending change. |
| 11034 | 16 | No | Deletion of the row was canceled during notification. |
| 11036 | 16 | No | The rowset was using optimistic concurrency and the value of a column has been changed after the containing row was last fetched or resynchronized. |
| 11037 | 16 | No | The row has a pending delete or the deletion had been transmitted to the data source. |
| 11038 | 16 | No | The row is a pending insert row. |
| 11039 | 16 | No | DBPROP_CHANGEINSERTEDROWS was VARIANT_FALSE and the insertion for the row has been transmitted to the data source. |
| 11040 | 16 | No | Deleting the row violated the integrity constraints for the column or table. |
| 11041 | 16 | No | The row handle was invalid or was a row handle to which the current thread does not have access rights. |
| 11042 | 16 | No | Deleting the row would exceed the limit for pending changes specified by the rowset property DBPROP_MAXPENDINGROWS. |
| 11043 | 16 | No | The row has a storage object open. |
| 11044 | 16 | No | The provider ran out of memory and could not fetch the row. |
| 11045 | 16 | No | User did not have sufficient permission to delete the row. |
| 11046 | 16 | No | The table was in immediate-update mode and the row was not deleted due to reaching a limit on the server, such as query execution timing out. |
| 11047 | 16 | No | Updating did not meet the schema requirements. |
| 11048 | 16 | No | There was a recoverable, provider-specific error, such as an RPC failure. |
| 11100 | 16 | No | The provider indicates that conflicts occurred with other properties or requirements. |
| 11101 | 16 | No | Could not obtain an interface required for text, ntext, or image access. |
| 11102 | 16 | No | The provider could not support a required row lookup interface. |
| 11103 | 16 | No | The provider could not support an interface required for the UPDATE/DELETE/INSERT statements. |
| 11104 | 16 | No | The provider could not support insertion on this table. |
| 11105 | 16 | No | The provider could not support updates on this table. |
| 11106 | 16 | No | The provider could not support deletion on this table. |
| 11107 | 16 | No | The provider could not support a row lookup position. |
| 11108 | 16 | No | The provider could not support a required property. |
| 11109 | 16 | No | The provider does not support an index scan on this data source. |
| 11201 | 16 | No | This message could not be delivered because the FROM service name is missing. The message origin is: '%ls'. |
| 11202 | 16 | No | This message has been dropped because the FROM service name exceeds the maximum size of %d bytes. Service name: "%.\*ls". Message origin: "%ls". |
| 11203 | 16 | No | This message has been dropped because the FROM broker instance is missing. The message origin is '%ls'. |
| 11204 | 16 | No | This message has been dropped because the FROM broker instance exceeds the maximum size of %d bytes. Broker instance: "%.\*ls". Message origin: "%ls". |
| 11205 | 16 | No | This message has been dropped because the TO service name is missing. The message origin is "%ls". |
| 11206 | 16 | No | This message has been dropped because the TO service name exceeds the maximum size of %d bytes. Service name: "%.\*ls". Message origin: "%ls". |
| 11207 | 16 | No | This message has been dropped because the service contract name is missing. The message origin is "%ls". |
| 11208 | 16 | No | This message has been dropped because the service contract name exceeds the maximum size of %d bytes. Contract name "%.\*ls". Message origin: "%ls". |
| 11209 | 16 | No | This message could not be delivered because the conversation ID could not be associated with an active conversation. The message origin is: '%ls'. |
| 11210 | 16 | No | This message has been dropped because the TO service could not be found. Service name: "%.\*ls". Message origin: "%ls". |
| 11211 | 16 | No | This message has been dropped because the user does not have permission to access the target database. Database ID: %d. Message origin: &amp;quot;%ls&amp;quot;. |
| 11212 | 16 | No | This message could not be delivered because the conversation endpoint has already been closed. |
| 11213 | 16 | No | This message could not be delivered because this is not the first message in the conversation. |
| 11214 | 16 | No | This message could not be delivered because the '%.\*ls' contract could not be found or the service does not accept conversations for the contract. |
| 11215 | 16 | No | This message could not be delivered because the user with ID %i in database ID %i does not have permission to send to the service. Service name: '%.\*ls'. |
| 11216 | 16 | No | This message could not be delivered because there is already another task processing this message. |
| 11217 | 16 | No | This message could not be delivered because it is out of sequence with respect to the conversation. Conversation receive sequence number: %I64d, Message sequence number: %I64d. |
| 11218 | 16 | No | This message could not be delivered because it is a duplicate. |
| 11219 | 16 | No | This message could not be delivered because the destination queue has been disabled. Queue ID: %d. |
| 11220 | 16 | No | This message could not be delivered because the TO broker instance is missing. |
| 11221 | 16 | No | This message could not be delivered because there is an inconsistency in the message header. |
| 11222 | 16 | No | This message could not be delivered because the TO service name in the message does not match the name in the conversation endpoint. Message TO Service Name: '%.\*ls'. Conversation Endpoint TO Service Name: '%.\*ls'. |
| 11223 | 16 | No | This message could not be delivered because the service contract name in the message does not match the name in the conversation endpoint. Message service contract name: '%.\*ls'. Conversation endpoint service contract name: '%.\*ls'. |
| 11224 | 16 | No | This message could not be delivered because another instance of this service program has already started conversing with this endpoint. |
| 11225 | 16 | No | This message could not be delivered because the message type name could not be found. Message type name: '%.\*ls'. |
| 11226 | 16 | No | This message could not be delivered because the message type is not part of the service contract. Message type name: '%.\*ls'. Service contract name: '%.\*ls'. |
| 11227 | 16 | No | This message could not be delivered because the initiator service has sent a message with a message type that can only be sent by the target. Message type name: '%.\*ls'. Service contract name: '%.\*ls'. |
| 11228 | 16 | No | This message could not be delivered because the target service has sent a message with a message type that can only be sent by the initiator. Message type name: '%.\*ls'. Service contract name: '%.\*ls'. |
| 11229 | 16 | No | This message could not be delivered because the security context could not be retrieved. |
| 11230 | 16 | No | This message could not be delivered because the message could not be decrypted and validated. |
| 11231 | 16 | No | This message could not be delivered because the conversation endpoint is not secured, however the message is secured. |
| 11232 | 16 | No | This message could not be delivered because the conversation endpoint is secured, however the message is not secured. |
| 11233 | 16 | No | This message has been dropped because the session key of the conversation endpoint does not match that of the message. |
| 11234 | 16 | No | This message could not be delivered because an internal error was encountered while processing it. Error code %d, state %d: %.\*ls. |
| 11235 | 16 | No | Received a malformed message. The binary message class (%d:%d) is not defined. This may indicate network problems or that another application is connected to the Service Broker endpoint. |
| 11236 | 16 | No | A corrupted message has been received. The binary header size of %d is expected, however the header size received was %d. |
| 11237 | 16 | No | A %S_MSG message could not be processed due to insufficient memory. The message was dropped. |
| 11238 | 16 | No | A corrupted message has been received. The private variable data segment is malformed. |
| 11239 | 16 | No | A corrupted message has been received. The private variable data segment extends beyond the length of the message. |
| 11240 | 16 | No | A corrupted message has been received. The binary message preamble is malformed. |
| 11241 | 16 | No | A corrupted message has been received. The conversation security version number is not %d.%d. |
| 11242 | 16 | No | A corrupted message has been received. The maximum number of public variable data elements (%d) has been exceeded. Public variable data elements found: %d. |
| 11243 | 16 | No | A corrupted message has been received. The public variable data element (%d) has been duplicated in this message. |
| 11244 | 16 | No | A corrupted message has been received. The handshake validation header is malformed. |
| 11245 | 16 | No | A corrupted message has been received. The maximum number of private variable data elements (%d) has been exceeded. Private variable data elements found: %d. |
| 11246 | 16 | No | A corrupted message has been received. The private variable data element (%d) has been duplicated in this message. |
| 11247 | 16 | No | A corrupted message has been received. The login negotiate header is invalid. |
| 11248 | 16 | No | A corrupted message has been received. The SSPI login header is invalid. |
| 11249 | 16 | No | A corrupted message has been received. The pre-master-secret is invalid. |
| 11250 | 16 | No | A corrupted message has been received. The security certificate key fields must both be present or both be absent. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11251 | 16 | No | A corrupted message has been received. The service pair security header source certificate and the signature must both be present or both be absent. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11252 | 16 | No | A corrupted message has been received. The destination certificate serial number is missing. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11253 | 16 | No | A corrupted message has been received. The service pair security header destination certificate, the key exchange key, the key exchange key ID, and the session key must all be present or all be absent. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11254 | 16 | No | A corrupted message has been received. The session key ID is missing. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11255 | 16 | No | A corrupted message has been received. The encryption flag is set, however the message body, MIC or salt is missing. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11256 | 16 | No | A corrupted message has been received. The MIC is present, however the message body or encryption flag is missing. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11257 | 16 | No | A corrupted message has been received. The MIC and session key ID are in an invalid state. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11258 | 16 | No | A corrupted message has been received. The MIC size is %d, however it must be no greater than %d bytes in length. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11259 | 16 | No | A corrupted message has been received. The certificate serial number size is %d, however it must be no greater than %d bytes in length. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11260 | 16 | No | A corrupted message has been received. The certificate issuer name size is %d, however it must be no greater than %d bytes in length. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11261 | 16 | No | A corrupted message has been received. The destination certificate serial number size is %d, however it must be no greater than %d bytes in length. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11262 | 16 | No | A corrupted message has been received. The destination certificate issuer name size is %d, however it must be no greater than %d bytes in length. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11263 | 16 | No | A corrupted message has been received. The service pair security header size is %d, however it must be between %d and %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11264 | 16 | No | A corrupted message has been received. The key exchange key size is %d, however it must be between %d and %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11265 | 16 | No | A corrupted message has been received. The key exchange key ID is invalid. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11266 | 16 | No | A corrupted message has been received. The encrypted session key size is %d, however it must be %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11267 | 16 | No | A corrupted message has been received. The session key ID size is %d, however it must be %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11268 | 16 | No | A corrupted message has been received. The salt size is %d, however it must be %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11269 | 16 | No | A corrupted message has been received. A UNICODE string is not two byte aligned within the message. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11270 | 16 | No | A corrupted message has been received. A UNICODE string is greater than the maximum allowed size of %d bytes. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11271 | 16 | No | A corrupted message has been received. The conversation ID must not be NULL. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11272 | 16 | No | A corrupted message has been received. The message ID must not be NULL. |
| 11273 | 16 | No | A corrupted message has been received. The message body is not properly padded for encryption. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11274 | 16 | No | A corrupted message has been received. A sequence number is larger than allowed. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11275 | 16 | No | A corrupted message has been received. The End of Conversation and Error flags are both set. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11276 | 16 | No | A corrupted message has been received. The End of Conversation flag has been set on an unsequenced message. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11277 | 16 | No | A corrupted message has been received. The End of Conversation and Error flags may not be set in the first sequenced message. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11278 | 16 | No | A corrupted message has been received. The message type is missing for this message. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11279 | 16 | No | A corrupted message has been received. The message type must not be set in this message. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11280 | 16 | No | A packet of size %lu bytes could not be processed because it exceeds the receive buffer count. |
| 11281 | 16 | No | A corrupted message has been received. The private portion of the message header is malformed. |
| 11282 | 16 | No | This message has been dropped due to licensing restrictions. See the documentation for further details. |
| 11285 | 16 | No | This forwarded message has been dropped because the hops remaining count has reached 0. |
| 11286 | 16 | No | Dropped this forwarded message because this SQL Server instance is out of memory. |
| 11288 | 16 | No | This forwarded message has been dropped because a duplicate message is already being forwarded. |
| 11289 | 16 | No | This forwarded message has been dropped because its memory usage would exceed the configured memory limit of %d bytes for forwarded messages. |
| 11290 | 16 | No | This forwarded message was dropped because the message could not be delivered within the message time to live. This may indicate that the forwarding route is incorrectly configured or that the destination is unavailable. |
| 11291 | 16 | No | This forwarded message has been dropped because the time consumed has exceeded the message's time to live of %u seconds (the message arrived with %u seconds consumed and used %u seconds in this broker). |
| 11292 | 16 | No | The forwarded message has been dropped because a transport send error occurred when sending the message. Check previous events for the error. |
| 11293 | 16 | No | This forwarded message has been dropped because a transport is shutdown. |
| 11294 | 16 | No | This forwarded message has been dropped because the destination route is not valid. |
| 11295 | 10 | No | Endpoint configuration change detected. Service Broker manager and transport will now restart. |
| 11296 | 10 | No | Certificate change detected. Service Broker manager and transport will now restart. |
| 11297 | 16 | No | A corrupted message has been received. The private variable data segment offset is incorrect. |
| 11298 | 16 | No | A corrupted message has been received. The public variable data segment offset is incorrect. |
| 11299 | 10 | No | A corrupted message has been received. An unsequenced message had a non-zero sequence number. This occurred in the message with Conversation ID '%.\*ls', Initiator: %d, and Message sequence number: %I64d. |
| 11300 | 10 | Yes | Error wile committing a readonly or a TEMPDB XDES, Shutting down the server. |
| 11301 | 10 | Yes | Error while performing transaction notification for object %p event %d. |
| 11302 | 10 | Yes | Error during rollback. shutting down database (location: %d). |
| 11303 | 10 | Yes | Error releasing reserved log space: %ls space %I64d, code %d, state %d. |
| 11304 | 10 | Yes | Failed to record outcome of a local two-phase commit transaction. Taking database offline. |
| 11306 | 16 | No | Forward progress on this transaction is disallowed. Transaction has been rolled back. |
| 11313 | 16 | No | This operation must be executed within a parallel nested transaction. |
| 11314 | 16 | No | The stored procedure %.\*ls must be executed within a user transaction. |
| 11315 | 16 | No | The isolation level specified for the PNT child transaction does not match the current isolation level for the parent. |
| 11316 | 16 | No | %ls statement cannot be used inside a parallel nested transaction. |
| 11317 | 16 | No | Parallel plan with updates is not supported inside a parallel nested transaction. |
| 11318 | 16 | No | The stored procedure '%.\*ls' cannot be executed through MARS connection. |
| 11319 | 16 | No | Bound sessions and user parallel nested transactions cannot be used in the same transaction. |
| 11320 | 16 | No | Cannot create a User Parallel Nested Transaction, the maximum number of parallel nested transactions is reached. |
| 11321 | 16 | No | This operation cannot be executed within an active transaction. |
| 11322 | 16 | No | Controlling explicit transactions and creating savepoints (BEGIN/SAVE/COMMIT/ROLLBACK TRANSACTION) is not supported inside ATOMIC blocks. |
| 11323 | 16 | No | Memory-optimized tables and natively compiled modules cannot be used inside non-natively compiled ATOMIC blocks. |
| 11324 | 16 | No | @@TRANCOUNT is not supported inside ATOMIC blocks. |
| 11325 | 16 | No | Multiple Active Result Sets (MARS) and bound sessions are not supported inside ATOMIC blocks. |
| 11400 | 16 | No | ALTER TABLE SWITCH statement failed. Index '%.\*ls' on indexed view '%.\*ls' uses partition function '%.\*ls', but table '%.\*ls' uses non-equivalent partition function '%.\*ls'. Index on indexed view '%.\*ls' and table '%.\*ls' must use an equivalent partition function. |
| 11401 | 16 | No | ALTER TABLE SWITCH statement failed. Table '%.\*ls' is %S_MSG, but index '%.\*ls' on indexed view '%.\*ls' is %S_MSG. |
| 11402 | 16 | No | ALTER TABLE SWITCH statement failed. Target table '%.\*ls' is referenced by %d indexed view(s), but source table '%.\*ls' is only referenced by %d indexed view(s). Every indexed view on the target table must have at least one matching indexed view on the source table. |
| 11403 | 16 | No | ALTER TABLE SWITCH statement failed. Indexed view '%.\*ls' is not aligned with table '%.\*ls'. The partitioning column '%.\*ls' from the indexed view calculates its value from one or more columns or an expression, rather than directly selecting from the table partitioning column '%.\*ls'. Change the indexed view definition, so that the partitioning column is directly selected from table partitioning column '%.\*ls'. |
| 11404 | 16 | No | ALTER TABLE SWITCH statement failed. Target table '%.\*ls' is referenced by %d indexed view(s), but source table '%.\*ls' is only referenced by %d matching indexed view(s). Every indexed view on the target table must have at least one matching indexed view on the source table. |
| 11405 | 16 | No | ALTER TABLE SWITCH statement failed. Table '%.\*ls' is not aligned with the index '%.\*ls' on indexed view '%.\*ls'. The table is partitioned on column '%.\*ls', but the index on the indexed view is partitioned on column '%.\*ls', which is selected from a different column '%.\*ls' in table '%.\*ls'. Change the indexed view definition so that the partitioning column is the same as the table's partitioning column. |
| 11406 | 16 | No | ALTER TABLE SWITCH statement failed. Source and target partitions have different values for the DATA_COMPRESSION option. |
| 11407 | 16 | No | Vardecimal storage format can not be enabled for '%.\*ls'. Only Enterprise edition of SQL Server supports vardecimal. |
| 11408 | 16 | No | Cannot modify the column '%.\*ls' in the table '%.\*ls' to add or remove the COLUMN_SET attribute. To change a COLUMN_SET attribute of a column, either modify the table to remove the column and then add the column again, or drop and re-create the table. |
| [11409](../mssqlserver-11409-database-engine-error.md) | 16 | No | Cannot remove the column set '%.\*ls' in the table '%.\*ls' because the table contains more than 1025 columns. Reduce the number of columns in the table to less than 1025. |
| 11410 | 16 | No | Cannot modify the column '%.\*ls' in the table '%.\*ls' to a sparse column because the column has a default or rule bound to it. Unbind the rule or default from the column before designating the column as sparse. |
| 11411 | 16 | No | Cannot add the sparse column '%.\*ls' to the table '%.\*ls' because the data type of the column has a default or rule bound to it. Unbind the rule or default from the data type before adding the sparse column to the table. |
| 11412 | 16 | No | ALTER TABLE SWITCH statement failed because column '%.\*ls' does not have the same sparse storage attribute in tables '%.\*ls' and '%.\*ls'. |
| 11413 | 16 | No | ALTER TABLE SWITCH statement failed because column '%.\*ls' does not have the same column set property in tables '%.\*ls' and '%.\*ls'. |
| 11414 | 10 | No | Warning: Option %ls is not applicable to table %.\*ls because it does not have a clustered index. This option will be applied only to the table's nonclustered indexes, if it has any. |
| 11415 | 16 | No | Object '%.\*ls' cannot be disabled or enabled. This action applies only to foreign key and check constraints. |
| 11418 | 16 | No | Cannot %S_MSG table '%.\*ls' because the table either contains sparse columns or a column set column which are incompatible with compression. |
| 11419 | 16 | No | Cannot alter or drop column '%.\*ls' because the table '%.\*ls' is federated on it. |
| 11420 | 16 | No | ALTER TABLE SWITCH statement failed. Indexed view '%.\*ls' references an object that does not participate in the ALTER TABLE SWITCH statement, therefore the WAIT_AT_LOW_PRIORITY option cannot be used. Drop the indexes of this view or change its definition to reference only tables that participate in the ALTER TABLE SWITCH statement. |
| 11421 | 10 | Yes | An '%.\*ls' statement was executed on database '%.\*ls', table '%.\*ls' by hostname '%.\*ls', host process ID %d using the WAIT_AT_LOW_PRIORITY options with MAX_DURATION = %d and ABORT_AFTER_WAIT = BLOCKERS. Blocking user sessions will be killed after the max duration of waiting time. |
| 11422 | 10 | Yes | An ALTER TABLE SWITCH statement was executed on database '%.\*ls', table '%.\*ls' by hostname '%.\*ls', host process ID %d with target table '%.\*ls' using the WAIT_AT_LOW_PRIORITY options with MAX_DURATION = %d and ABORT_AFTER_WAIT = BLOCKERS. Blocking user sessions will be killed after the max duration of waiting time. |
| 11423 | 14 | No | User does not have permission to use the ABORT_AFTER_WAIT = BLOCKERS option. |
| 11424 | 16 | No | Cannot alter the identity column '%.\*ls' in the table '%.\*ls' because this operation requires data modification and the table contains a persisted computed column. Remove the persisted computed column before modifying the identity column. |
| 11425 | 16 | No | Could not proceed with the DDL operation because it is referencing column '%.\*ls' on table '%.\*ls' and this conflicts with a concurrent column operation that is in progress on this table. The concurrent operation could be an online alter column operation. |
| 11426 | 16 | No | Cannot alter a column on a local temporary table online. Perform the alter operation offline. |
| 11427 | 16 | No | The online ALTER COLUMN operation cannot be performed for table '%.\*ls' because column '%.\*ls' currently has or is getting altered into an unsupported datatype: text, ntext, image, CLR type or FILESTREAM. The operation must be performed offline. |
| 11428 | 16 | No | Column '%.\*ls' cannot be altered online to an XML type that has a schema collection. The operation must be performed offline. |
| 11429 | 16 | No | The online ALTER COLUMN statement failed for table '%.\*ls' because the table has change tracking enabled or is marked for merge replication. Disable change tracking and merge replication before using online ALTER COLUMN or perform the operation offline. |
| 11430 | 16 | No | Cannot enable change data capture on column '%.\*ls'. Change data capture is not supported for encrypted columns. |
| 11601 | 15 | No | %ls statements with a '%.\*ls' option are not allowed. |
| 11602 | 10 | No | %ls statements are not verified. |
| 11603 | 15 | No | %ls statements are not allowed at the top level. |
| 11605 | 15 | No | %S_MSG are not allowed at the top level. |
| 11606 | 15 | No | Specifying server name in '%.\*ls' is not allowed. |
| 11607 | 15 | No | Specifying database name for '%.\*ls' in a %ls statement is not allowed. |
| 11608 | 15 | No | Creating temporary stored procedures is not allowed. |
| 11609 | 16 | No | An internal error occurred while building the project. %ls |
| 11610 | 16 | No | There is not enough memory to build the project. |
| 11611 | 15 | No | Specifying schema elements in the CREATE SCHEMA statement is not supported. |
| 11612 | 15 | No | Multiple statements in a T-SQL batch are not allowed at the top level. |
| 11613 | 15 | No | Numbered stored procedures are not supported. |
| 11614 | 15 | No | %ls is not supported. |
| 11617 | 16 | No | An unknown error has occurred trying to load '%hs'. |
| 11618 | 15 | No | Combining column level permissions with other permissions is not allowed in the same GRANT/DENY/REVOKE statement. |
| 11619 | 16 | No | There is not enough stack available to compile the statment. |
| 11620 | 15 | No | REVOKE statements can only be used to revoke column level permissions. |
| 11621 | 10 | No | SQL Server started in Language Service mode. |
| 11622 | 16 | No | CREATE ASSEMBLY can only be created FROM a constant binary expression. |
| 11623 | 15 | No | ALTER TABLE statements can only be used to add a single constraint. |
| 11624 | 15 | No | ALTER ROLE statements can only be used to add a member to a role. |
| 11625 | 16 | No | '%ls' is either corrupt, not readable or not accessible. |
| 11651 | 10 | No | %ls statements with a '%.\*ls' option are not supported in a data-tier application. |
| 11652 | 10 | No | %ls statements are not supported at the top level in a data-tier application. |
| 11653 | 10 | No | Cannot execute as the user '%.\*ls' because it does not exist. |
| 11700 | 16 | No | The increment for sequence object '%.\*ls' cannot be zero. |
| 11701 | 16 | No | The absolute value of the increment for sequence object '%.\*ls' must be less than or equal to the difference between the minimum and maximum value of the sequence object. |
| 11702 | 16 | No | The sequence object '%.\*ls' must be of data type int, bigint, smallint, tinyint, or decimal or numeric with a scale of 0, or any user-defined data type that is based on one of the above integer data types. |
| 11703 | 16 | No | The start value for sequence object '%.\*ls' must be between the minimum and maximum value of the sequence object. |
| 11704 | 16 | No | The current value '%.\*ls' for sequence object '%.\*ls' must be between the minimum and maximum value of the sequence object. |
| 11705 | 16 | No | The minimum value for sequence object '%.\*ls' must be less than its maximum value. |
| 11706 | 16 | No | The cache size for sequence object '%.\*ls' must be greater than 0. |
| 11707 | 10 | No | The cache size for sequence object '%.\*ls' has been set to NO CACHE. |
| 11708 | 16 | No | An invalid value was specified for argument '%.\*ls' for the given data type. |
| 11709 | 15 | No | The 'RESTART WITH' argument cannot be used in a CREATE SEQUENCE statement. |
| 11710 | 15 | No | Argument 'START WITH' cannot be used in an ALTER SEQUENCE statement. |
| 11711 | 15 | No | Argument 'AS' cannot be used in an ALTER SEQUENCE statement. |
| 11712 | 15 | No | Argument '%.\*ls' can not be specified more than once. |
| 11714 | 15 | No | Invalid sequence name '%.\*ls'. |
| 11715 | 15 | No | No properties specified for ALTER SEQUENCE. |
| 11716 | 15 | No | NEXT VALUE FOR function does not support the PARTITION BY clause. |
| 11717 | 15 | No | NEXT VALUE FOR function does not support the OVER clause in default constraints, UPDATE statements, or MERGE statements. |
| 11718 | 15 | No | NEXT VALUE FOR function does not support an empty OVER clause. |
| 11719 | 15 | No | NEXT VALUE FOR function is not allowed in check constraints, default objects, computed columns, views, user-defined functions, user-defined aggregates, user-defined table types, sub-queries, common table expressions, derived tables or return statements. |
| 11720 | 15 | No | NEXT VALUE FOR function is not allowed in the TOP, OVER, OUTPUT, ON, WHERE, GROUP BY, HAVING, or ORDER BY clauses. |
| 11721 | 15 | No | NEXT VALUE FOR function cannot be used directly in a statement that uses a DISTINCT, UNION, UNION ALL, EXCEPT or INTERSECT operator. |
| 11722 | 15 | No | NEXT VALUE FOR function is not allowed in the WHEN MATCHED clause, the WHEN NOT MATCHED clause, or the WHEN NOT MATCHED BY SOURCE clause of a merge statement. |
| 11723 | 15 | No | NEXT VALUE FOR function cannot be used directly in a statement that contains an ORDER BY clause unless the OVER clause is specified. |
| 11724 | 15 | No | An expression that contains a NEXT VALUE FOR function cannot be passed as an argument to a table-valued function. |
| 11725 | 15 | No | An expression that contains a NEXT VALUE FOR function cannot be passed as an argument to an aggregate. |
| 11726 | 16 | No | Object '%.\*ls' is not a sequence object. |
| 11727 | 16 | No | NEXT VALUE FOR functions for a given sequence object must have exactly the same OVER clause definition. |
| 11728 | 16 | No | The sequence object '%.\*ls' has reached its minimum or maximum value. Restart the sequence object to allow new values to be generated. |
| 11729 | 10 | No | The sequence object '%.\*ls' cache size is greater than the number of available values. |
| 11730 | 16 | No | Database name cannot be specified for the sequence object in default constraints. |
| 11731 | 16 | No | A column that uses a sequence object in the default constraint must be present in the target columns list, if the same sequence object appears in a row constructor. |
| 11732 | 16 | No | The requested range for sequence object '%.\*ls' exceeds the maximum or minimum limit. Retry with a smaller range. |
| 11733 | 16 | No | Parameter '%.\*ls' must be a positive integer. |
| 11734 | 16 | No | NEXT VALUE FOR function is not allowed in the SELECT clause when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 11735 | 16 | No | The target table of the INSERT statement cannot have DEFAULT constraints using the NEXT VALUE FOR function when the FROM clause contains a nested INSERT, UPDATE, DELETE, or MERGE statement. |
| 11736 | 16 | No | Only one instance of NEXT VALUE FOR function per sequence object is allowed in SET or SELECT with variable assignment. |
| 11737 | 15 | No | NEXT VALUE FOR function does not support the ROWS and RANGE clauses. |
| 11738 | 16 | No | The use of NEXT VALUE FOR function is not allowed in this context. |
| 11739 | 16 | No | NEXT VALUE FOR function cannot be used if ROWCOUNT option has been set, or the query contains TOP or OFFSET. |
| 11740 | 16 | No | NEXT VALUE FOR function cannot be used in a default constraint if ROWCOUNT option has been set, or the query contains TOP or OFFSET. |
| 11741 | 16 | No | NEXT VALUE FOR function cannot be used within CASE, CHOOSE, COALESCE, IIF, ISNULL and NULLIF. |
| 11742 | 16 | No | NEXT VALUE FOR function can only be used with MERGE if it is defined within a default constraint on the target table for insert actions. |
| 11743 | 16 | No | Timeout occurred while waiting for METADATA_SEQUENCE_GENERATOR latch: waittime %d seconds. |
| 11800 | 16 | No | RESTORE WITH SNAPSHOTRESTOREPHASE=2 for database '%ls' failed because an earlier RESTORE WITH SNAPSHOTRESTOREPHASE=1 may have failed as a result of a network error. Retry the restore operation through SQL Writer after addressing any network issues and making sure that SQL Server is running. |
| 11901 | 16 | No | Column '%.\*ls.%.\*ls' is a federated column, while referencing column '%.\*ls.%.\*ls' in foreign key '%.\*ls' is not. |
| 11902 | 16 | No | Federation scheme key '%.\*ls' is not a part of this federation. |
| 12002 | 16 | No | The requested %S_MSG index on column '%.\*ls' of table '%.\*ls' could not be created because the column type is not %S_MSG . Specify a column name that refers to a column with a %S_MSG data type. |
| 12003 | 16 | No | Could not find spatial tessellation scheme '%.\*ls' for column of type %.\*ls. Specify a valid tessellation scheme name in your USING clause. |
| 12004 | 16 | No | Could not find the default spatial tessellation scheme for the column '%.\*ls' on table '%.\*ls'. Make sure that the column reference is correct, or specify the extension scheme in a USING clause. |
| 12005 | 16 | No | Incorrect parameters were passed to the CREATE %S_MSG statement near '%.\*ls'. Validate the statement against the index-creation syntax. |
| 12006 | 16 | No | Duplicate parameters were passed to the create index statement. Validate the statement against the index-creation syntax. |
| 12007 | 16 | No | The CREATE %S_MSG statement is missing the required parameter '%.\*ls'. Validate the statement against the index-creation syntax. |
| 12008 | 16 | No | Table '%.\*ls' does not have a clustered primary key as required by the %S_MSG index. Make sure that the primary key column exists on the table before creating a %S_MSG index. |
| 12009 | 16 | No | Could not find the %S_MSG index '%.\*ls' on table '%.\*ls'. Either no %S_MSG index with this name exists, or a non-%S_MSG index might be using the same name. Fix the index name, avoiding duplicates. If a relational index has the same name, drop the regular relational index. |
| 12010 | 16 | No | Only one spatial index hint may appear per table, either as the first or the last hinted index. |
| 12011 | 16 | No | The value of parameter '%.\*ls' of CREATE %S_MSG must be less than %d. |
| 12012 | 16 | No | The value of parameter '%.\*ls' of CREATE %S_MSG must be greater than %d. |
| 12013 | 16 | No | The value of parameter '%.\*ls' of CREATE %S_MSG must be greater than the value of parameter '%.\*ls'. |
| 12014 | 16 | No | The '%.\*ls' parameter of CREATE %S_MSG is incompletely defined. If the parameter has more than one part, all the parts must be defined. |
| 12015 | 16 | No | The index option %.\*ls in the CREATE %S_MSG statement has to appear before the general index options. |
| 12016 | 16 | No | Creating a %S_MSG index requires that the primary key in the base table satisfy the following restrictions. The maximum number of primary-key columns is %d. The maximum combined per-row size of the primary-key columns is %d bytes. The primary key on the base table '%.\*ls' has %d columns, and contains %d bytes. Alter the base table to satisfy the primary-key restrictions imposed by the %S_MSG index. |
| 12017 | 10 | No | The spatial index is disabled or offline |
| 12018 | 10 | No | The spatial object is not defined in the scope of the predicate |
| 12019 | 10 | No | Spatial indexes do not support the comparand supplied in the predicate |
| 12020 | 10 | No | Spatial indexes do not support the comparator supplied in the predicate |
| 12021 | 10 | No | Spatial indexes do not support the method name supplied in the predicate |
| 12022 | 10 | No | The comparand references a column that is defined below the predicate |
| 12023 | 10 | No | The comparand in the comparison predicate is not deterministic |
| 12024 | 10 | No | The spatial parameter references a column that is defined below the predicate |
| 12025 | 10 | No | Could not find required binary spatial method in a condition |
| 12026 | 10 | No | Could not find required comparison predicate |
| 12100 | 16 | No | ALTER DATABASE failed because FILESTREAM filegroups cannot be added to a database that has either the READ_COMMITTED_SNAPSHOT or the ALLOW_SNAPSHOT_ISOLATION option set to ON. To add FILESTREAM filegroups, you must set READ_COMMITTED_SNAPSHOT and ALLOW_SNAPSHOT_ISOLATION to OFF. |
| 12101 | 16 | No | Cannot disable change tracking on database '%.\*ls' while client connections are waiting on change notification. Please close those connections before disabling change tracking. |
| 12102 | 16 | No | ALTER DATABASE failed because the distribution policy of system databases cannot be changed. |
| 12103 | 16 | No | ALTER DATABASE failed because the distribution policy is invalid. The database distribution policy must be set to either NONE or HASH. For the distribution policy NONE, the number of leading hash columns cannot be specified. For the distribution policy HASH, the number of leading hash columns is optional but cannot be more than 16 columns. |
| 12104 | 15 | No | ALTER DATABASE CURRENT failed because '%.\*ls' is a system database. System databases cannot be altered by using the CURRENT keyword. Use the database name to alter a system database. |
| 12105 | 10 | No | Waiting for the nonqualified transactions to be rolled back on the remote brick %d. |
| 12106 | 16 | No | The path name '%.\*ls' is already used by another database file. Change to another valid and UNUSED name. |
| 12107 | 16 | No | Adding a MEMORY_OPTIMIZED_DATA filegroup is not supported for databases that have one or more publications that use sync_method 'database snapshot' or 'database snapshot character'. |
| 12108 | 16 | No | '%d' is out of range for the database scoped configuration option '%.\*ls'. See sp_configure option '%ls' for valid values. |
| 12109 | 16 | No | Statement '%.\*ls' failed, because it attempted to set the value to '%.\*ls' for the primary replica. A settings can only be set to '%.\*ls' when the setting is applied to the secondary. |
| [12300](../mssqlserver-12300-database-engine-error.md) | 15 | No | Computed columns are not supported with %S_MSG. |
| [12301](../mssqlserver-12301-database-engine-error.md) | 15 | No | Nullable columns in the index key are not supported with %S_MSG. |
| [12302](../mssqlserver-12302-database-engine-error.md) | 15 | No | Updating columns that are part of the PRIMARY KEY constraint is not supported with %S_MSG. |
| [12303](../mssqlserver-12303-database-engine-error.md) | 15 | No | The 'number' clause is not supported with %S_MSG. |
| [12304](../mssqlserver-12304-database-engine-error.md) | 15 | No | Updating columns that are part of a UNIQUE KEY constraint or a UNIQUE index is not supported with %S_MSG. |
| [12305](../mssqlserver-12305-database-engine-error.md) | 15 | No | Inline table variables are not supported with %S_MSG. |
| [12306](../mssqlserver-12306-database-engine-error.md) | 15 | No | Cursors are not supported with %S_MSG. |
| [12307](../mssqlserver-12307-database-engine-error.md) | 15 | No | Default values for parameters in %S_MSG must be constants. |
| [12308](../mssqlserver-12308-database-engine-error.md) | 15 | No | Table-valued functions are not supported with %S_MSG. |
| 12309 | 15 | No | Statements of the form INSERT...VALUES... that insert multiple rows are not supported with %S_MSG. |
| 12310 | 15 | No | Common Table Expressions (CTE) are not supported with %S_MSG. |
| 12311 | 15 | No | Subqueries (queries nested inside another query) is only supported in SELECT statements with %S_MSG. |
| 12312 | 15 | No | Partition functions are not supported with %S_MSG. |
| 12313 | 15 | No | User-defined functions are not supported with %S_MSG. |
| 12314 | 15 | No | User-defined methods are not supported with %S_MSG. |
| 12315 | 15 | No | User-defined properties are not supported with %S_MSG. |
| 12316 | 15 | No | User-defined aggregates are not supported with %S_MSG. |
| 12317 | 15 | No | Clustered indexes, which are the default for primary keys, are not supported with %S_MSG. Specify a NONCLUSTERED index instead. |
| 12318 | 15 | No | Browse mode metadata is not supported with %S_MSG. |
| 12319 | 15 | No | Using the FROM clause in an UPDATE statement and specifying a table source in a DELETE statement is not supported with %S_MSG. |
| 12320 | 15 | No | Operations that require a change to the schema version, for example renaming, are not supported with %S_MSG. |
| 12321 | 15 | No | Creating a temporary procedure is not supported with %S_MSG. |
| 12322 | 15 | No | Temporary tables are not supported with %S_MSG. |
| 12323 | 15 | No | Distributed Queries and Multiple Active Result Sets (MARS) are not supported with %S_MSG. |
| 12324 | 15 | No | Distributed transactions (DTC) are not supported with %S_MSG. |
| 12325 | 15 | No | Bound transactions are not supported with %S_MSG. |
| 12326 | 15 | No | Creating a savepoint is not supported with %S_MSG. |
| 12327 | 15 | No | Comparison, sorting, and manipulation of character strings that do not use a \*_BIN2 collation is not supported with %S_MSG. |
| 12328 | 15 | No | Indexes on character columns that do not use a \*_BIN2 collation are not supported with %S_MSG. |
| [12329](../mssqlserver-12329-database-engine-error.md) | 15 | No | The data types char(n) and varchar(n) using a collation that has a code page other than 1252 are not supported with %S_MSG. |
| 12330 | 15 | No | Truncation of character strings with an SC collation is not supported with %S_MSG. |
| 12331 | 15 | No | DDL statements ALTER, DROP and CREATE inside user transactions are not supported with %S_MSG. |
| 12332 | 15 | No | Database and server triggers on DDL statements CREATE, ALTER and DROP are not supported with %S_MSG. |
| 12333 | 15 | No | Execution from the dedicated administrator connection (DAC) is not supported with %S_MSG. |
| 12334 | 15 | No | The aggregate functions MIN and MAX used with binary and character string data types is not supported with %S_MSG. |
| 12336 | 15 | No | The use of replication is not supported with %S_MSG. |
| 12337 | 15 | No | The use of the sp_addpublication sync_method's parameters 'database snapshot' and 'database snapshot character' are not supported with %S_MSG. |
| 12338 | 15 | No | The functions LEN and SUBSTRING with an argument in an SC collation are not supported with %S_MSG. |
| 12339 | 15 | No | The use of seed and increment values other than 1 is not supported with %S_MSG. |
| 12340 | 15 | No | The EXECUTE statement in %S_MSG must use an object name. Variables and quoted identifiers are not supported. |
| 12341 | 15 | No | The WITH clause is not supported with EXECUTE statements in %S_MSG. |
| 12342 | 15 | No | The EXECUTE statement in %S_MSG only supports executing natively compiled modules. |
| 12343 | 16 | No | TRIGGER_NESTLEVEL only supports zero or one argument in %S_MSG. |
| 12344 | 16 | No | Only natively compiled modules can be used with %S_MSG. |
| 12345 | 16 | No | Max length data types are not supported as the return type of a natively compiled user defined function. |
| 12346 | 16 | No | Max length defaults are not supported with %S_MSG. |
| 12347 | 16 | No | Max length parameters to user defined functions are not supported in %S_MSG. |
| 12348 | 16 | No | Max length literals not supported in %S_MSG. |
| 12349 | 16 | No | Operation not supported for memory optimized tables having columnstore index. |
| 12350 | 15 | No | DML operations targeting table-valued functions are not supported with %S_MSG. |
| 12351 | 15 | No | Only natively compiled functions can be called with the EXECUTE from inside a natively compiled function. |
| 12358 | 15 | No | Enabling CDC creates database triggers on ALTER TABLE and DROP TABLE. Hence, these DDL statements are not supported with %S_MSG on CDC enabled databases. Other DDL triggers not related to CDC may also be blocking this operation. |
| 12401 | 15 | No | The %S_MSG option '%S_MSG' was specified more than once. Each option can be specified only once. |
| 12402 | 11 | No | Query with provided query_id (%ld) is not found in the Query Store for database (%ld). Check the query_id value and rerun the command. |
| 12403 | 11 | No | Query plan with provided plan_id (%ld) is not found in the Query Store for database (%ld). Check the plan_id value and rerun the command. |
| 12404 | 16 | No | The command failed because the query store is not in read-write mode for database (%ld). Make sure that the query store is in read-write mode and rerun the command. |
| 12405 | 16 | No | The command failed because the query store is not enabled for database (%ld). Make sure that the query store is enabled for the database and rerun the command. |
| 12406 | 11 | No | Query plan with provided plan_id (%ld) is not found in the Query Store for query (%ld). Check the plan_id value and rerun the command. |
| 12407 | 18 | No | The global instance of the the Query Store Manager is not available. |
| 12408 | 16 | No | An operation to read/write to the Query Store failed. Check the error logs to correct the source of the read/write failure |
| 12409 | 17 | No | Query Store cannot create system task |
| 12410 | 23 | No | Cannot load the Query Store metadata. Try turning the Query Store on manually, or contact customer support to get this addressed. |
| 12411 | 18 | No | Cannot load forced plan from the Query Store |
| 12412 | 16 | No | Internal table access error: failed to access the Query Store internal table with HRESULT: 0x%x. |
| 12413 | 16 | No | Cannot process statement SQL handle. Try querying the sys.query_store_query_text view instead. |
| 12414 | 16 | No | Failed to initialize Query Store for use, so user request cannot be executed. |
| 12415 | 16 | No | Failed to add query to Query Store for database ID %d. |
| 12417 | 15 | No | Only one Query Store option can be given in ALTER DATABASE statement. |
| 12418 | 16 | No | Mutually incompatible options for both database state change and for Query Store given in ALTER DATABASE statement. |
| 12419 | 16 | No | The command failed because Query Store is disabled on the server or database you are using. Contact customer support to get this addressed. |
| 12420 | 16 | No | Cannot perform action because Query Store is not started up for database %.\*ls. |
| 12421 | 14 | No | User does not have necessary permissions to execute Query Store stored procedure. |
| 12422 | 16 | No | Query Store interval length could not be changed because there is at least one existing runtime statistics interval set in the future. |
| 12423 | 16 | No | An operation to read/write to the Query Store failed. Partition or delete data, drop indexes, or consult the documentation for possible resolutions. |
| 12425 | 16 | No | Query with provided query id (%ld) cannot be deleted since it has active forcing policy. |
| 12426 | 16 | No | Plan with provided plan id (%ld) cannot be deleted since it has active forcing policy. |
| 12427 | 16 | No | Cannot perform operation on Query Store while it is enabled. Please turn off Query Store for the database and try again. |
| 12428 | 16 | No | The Query Store in database %.\*ls is missing internal table %.\*ls, possibly due to schema or catalog inconsistency. |
| 12429 | 16 | No | The Query Store in database %.\*ls has an invalid structure for internal table %.\*ls, possibly due to schema or catalog inconsistency. |
| 12430 | 16 | No | The specified Query Store action is not supported in stored procedure '%.\*ls'. |
| 12431 | 16 | No | Query Store stored procedure '%.\*ls' could not acquire an update lock over the database. |
| 12432 | 16 | No | Query Store Interval length cannot be changed because an invalid value was provided. Please try again with a valid value (1, 5, 10, 15, 30 & 60). |
| 12433 | 16 | No | Operation failed because Query Store %.\*ls is disabled on the server or database you are using. Contact customer support to get this addressed. |
| 12434 | 16 | No | The Query Store in database %.\*ls is invalid, possibly due to schema or catalog inconsistency. |
| 12435 | 16 | No | The Query Store in database %.\*ls has an invalid structure for internal table %.\*ls column %.\*ls, possibly due to schema or catalog inconsistency. |
| 12436 | 17 | No | Query Store global Resource Group cannot be determined. |
| 12437 | 17 | No | Query Store global Resource Group cannot be determined. |
| 12438 | 16 | No | Cannot perform action because Query Store cannot be enabled on system database %.\*ls. |
| 12439 | 10 | Yes | Setting database option query_store %ls to %lu for database '%.\*ls'. |
| 12440 | 10 | Yes | Setting database option query_store %ls to %ls for database '%.\*ls'. |
| 12441 | 10 | No | Query store is initializing.This is an informational message only; no user action is required. |
| 12442 | 17 | No | Query store flush failed due to internal error. |
| 12443 | 16 | Yes | Query store cannot set default settings. |
| 12444 | 16 | No | Query plan with plan_id (%ld) cannot be forced for query with query_id (%ld) as plan forcing is not supported for natively compiled plans. |
| 12600 | 16 | No | DBCC CLONEDATABASE is not allowed on this server. |
| 12601 | 16 | No | DBCC CLONEDATABASE is not allowed within a transaction. |
| 12602 | 16 | No | DBCC CLONEDATABASE cannot be executed through MARS connection. |
| 12603 | 16 | No | DBCC CLONEDATABASE does not support cloning system databases. |
| 12604 | 16 | No | Database cannot be read. Check if the database is in offline or suspect mode. |
| 12605 | 16 | No | Failed to create snapshot database. |
| 12606 | 16 | No | Failed to set snapshot database name. |
| 12607 | 16 | No | Specified clone database name '%.\*ls' is too long. |
| 12608 | 16 | No | Specified clone database name '%.\*ls' already exists. |
| 12609 | 16 | No | Failed to get file attributes. |
| 12610 | 16 | No | Failed to update database registration. |
| 12611 | 16 | No | Failed to get database registration attributes. |
| 12612 | 16 | No | Failed to sync boot page with database registration. |
| 12613 | 16 | No | Too many files or file groups to clone database. |
| 12614 | 16 | No | Failed to get collation name. |
| 12615 | 16 | No | Failed to get database properties. |
| 12616 | 16 | No | Failed to drop partially created cloned database. |
| 12617 | 16 | No | File path of the database is not supported. |
| 12618 | 16 | No | The database has too many objects. |
| 12619 | 16 | No | The database has too long file path to create clone. |
| 12620 | 10 | No | Database cloning for '%.\*ls' has started with target as '%.\*ls'. |
| 12621 | 10 | No | Database '%.\*ls' is a cloned database. This database should be used for diagnostic purposes only and is not supported for use in a production environment. |
| 12622 | 10 | No | Database cloning for '%.\*ls' has finished. Cloned database is '%.\*ls'. |
| 12623 | 10 | No | Clone backup succeeded and is stored in %ls. |
| 12624 | 10 | No | Clone backup failed. |
| 12625 | 10 | No | RESTORE VERIFY failed on the clone backup %ls |
| 12626 | 10 | No | Clone database verification has passed. |
| 12627 | 10 | No | Clone database verification has failed. |
| 12628 | 10 | No | NO_STATISTICS and NO_QUERYSTORE options turned ON as part of VERIFY_CLONE. |
| 12629 | 10 | No | Database '%.\*ls' is a cloned database. |
| 12630 | 16 | No | VERIFY_CLONE option cannot be specified together with SERVICEBROKER option. |
| 12800 | 16 | No | The reference to temp table name '%.\*ls' is ambiguous and cannot be resolved. Use either '%.\*ls' or '%.\*ls'. |
| 12801 | 16 | No | The reference to cursor name '%.\*ls' is ambiguous and cannot be resolved. Possible candidates are '%.\*ls' and '%.\*ls'. |
| 12803 | 16 | No | Containment cannot be enabled for database '%.\*ls' because it is a system database. |
| 12804 | 16 | No | Feature or option "%ls" breaches containment in a contained database. Please see Books Online topic Understanding Contained Databases for more information on contained databases. |
| 12805 | 16 | No | Index name '%.\*ls' is too long. Maximum length for temp table index name is %d characters. |
| 12807 | 16 | No | The option '%.\*ls' cannot be set on non-contained database. |
| 12808 | 16 | No | The option '%.\*ls' cannot be set on a database while containment is being set to NONE. |
| 12809 | 16 | No | You must remove all users with password before setting the containment property to NONE. |
| 12810 | 16 | No | The option '%.\*ls' was specified multiple times. |
| 12811 | 16 | No | The user options for the instance must be set to 0 in order to %S_MSG a contained database. |
| 12813 | 16 | No | Errors were encountered in the %S_MSG '%.\*ls' during compilation of the object. Either the containment option of the database '%.\*ls' was changed, or this object was present in model db and the user tried to create a new contained database. |
| 12814 | 16 | No | The object referenced as '%.\*ls' resolves differently in the target metadata collation '%.\*ls' than in the current metadata collation '%.\*ls'. |
| 12815 | 16 | No | The column referenced as '%.\*ls' resolves differently in the target metadata collation '%.\*ls' than in the current metadata collation '%.\*ls'. |
| 12816 | 16 | No | The type or XML schema collection referenced as '%.\*ls' resolves differently in the target metadata collation '%.\*ls' than in the current metadata collation '%.\*ls'. |
| 12817 | 16 | No | The reference to the variable, parameter or goto label '%.\*ls' resolves differently in the target metadata collation '%.\*ls' than in the current metadata collation '%.\*ls'. |
| 12818 | 16 | Yes | RECONFIGURE failed. Attempting to change the 'contained database authentication' value to 0 while there are existing contained databases requires a RECONFIGURE WITH OVERRIDE. |
| 12819 | 16 | No | sp_migrate_user_to_contained cannot be used in a non-contained database (a database with CONTAINMENT set to NONE). |
| 12820 | 16 | No | sp_migrate_user_to_contained can not be used with a user with a password or a user type other than SQL Login. |
| 12821 | 16 | No | sp_migrate_user_to_contained cannot be used on a user used in the EXECUTE AS clause of a signed module. |
| 12822 | 16 | No | sp_migrate_user_to_contained cannot be used to copy a password to an old hash algorithm. |
| 12823 | 16 | No | sp_migrate_user_to_contained can not find the login for user '%.\*ls'. |
| 12824 | 16 | No | The sp_configure value 'contained database authentication' must be set to 1 in order to %S_MSG a contained database. You may need to use RECONFIGURE to set the value_in_use. |
| 12825 | 16 | No | The database cannot be contained; this functionality is not available in the current edition of SQL Server. |
| 12826 | 16 | Yes | RECONFIGURE WITH OVERRIDE set the 'contained database authentication' to 0 while there are contained databases in use. This will disrupt authentication for contained users and will not allow new contained databases to be created. |
| 12827 | 16 | No | User-named %ls constraint '%.\*ls' is not allowed on temp table '%.\*ls' because it is being created in a contained database. Please consult the Books Online topic Understanding Contained Databases for more information on contained databases. |
| 12828 | 16 | No | User-defined %S_MSG '%.\*ls' in tempdb cannot be referenced from local temp table '%.\*ls' because the temp table is being created in a contained database. Please consult the Books Online topic Understanding Contained Databases for more information on contained databases. |
| 12829 | 16 | No | The stored procedure '%.\*ls' refers to a group of numbered stored procedures. Numbered stored procedures are not available in contained databases. Please consult the Books Online topic Understanding Contained Databases for more information on contained databases. |
| 12830 | 16 | No | The sp_configure 'user options' setting must be zero if the Database Engine has contained databases. |
| 12831 | 16 | No | Database '%.\*ls' is a contained database. The option 'contained database authentication' setting is 0. Users with passwords will not be able to login to contained databases. |
| 12832 | 16 | Yes | The database '%.\*ls' could not be created or altered to a contained database, because the schema bound %S_MSG '%.\*ls' depends on builtin function '%s'. In a contained database, the output collation of this builtin function has changed to '%.\*ls', which differs from the collation used in a non-contained database. |
| 12833 | 16 | Yes | The database '%.\*ls' could not be created or altered to a contained database, because the check constraint '%.\*ls' on table '%.\*ls' depends on builtin function '%s'. In a contained database, the output collation of this builtin function has changed to '%.\*ls', which differs from the collation used in a non-contained database. |
| 12834 | 16 | Yes | The database '%.\*ls' could not be created or altered to a contained database, because the computed column '%.\*ls' on %S_MSG '%.\*ls' depends on builtin function '%s'. In a contained database, the output collation of this builtin function has changed to '%.\*ls', which differs from the collation used in a non-contained database. |
| 12835 | 10 | Yes | The definition of the %S_MSG '%.\*ls' was refreshed as part of altering the containment option of the database '%.\*ls' because the object depends on builtin function '%s'. In a contained database, the output collation of this builtin function has changed to '%.\*ls', which differs from the collation used in a non-contained database. |
| 12836 | 16 | Yes | ALTER DATABASE statement failed. The containment option of the database '%.\*ls' could not be altered because compilation errors were encountered during validation of SQL modules. See previous errors. |
| 12837 | 16 | Yes | CREATE DATABASE statement failed. The contained database '%.\*ls' could not be created because compilation errors were encountered during validation of SQL modules. See previous errors. |
| 12838 | 16 | Yes | Replication, Change Data Capture and Change Tracking are not supported in contained databases. The database '%.\*ls' cannot be altered to a contained database, since it has one of these options turned on. |
| 12839 | 16 | Yes | Replication, Change Data Capture and Change Tracking are not supported in contained databases. The option cannot be enabled on the contained database '%s'. |
| 12840 | 16 | No | CREATE DATABASE failed. Recollating the database failed while creating the partially contained database '%.\*ls', with a default data collation of '%.\*ls'. |
| 12841 | 16 | No | ALTER DATABASE failed. Recollating the database failed while altering the database '%.\*ls' to containment='%ls'. |
| 12842 | 16 | No | The COLLATE CATALOG_DEFAULT clause cannot be used in a constraint, computed column, index filter expression, or any schema-bound object. |
| 12843 | 16 | Yes | The containment state of database '%.\*ls' does not match the value in master. Contained database functionality will not work as expected. Detach and re-attach the database to correct the database state in master. |
| 12980 | 16 | No | Supply either %s or %s to identify the log entries. |
| 12981 | 16 | No | You must specify %s when creating a subplan. |
| 12982 | 16 | No | Supply either %s or %s to identify the plan or sub-plan to be run. |
