---
title: Transactions (Azure Synapse Analytics and Microsoft Fabric)
description: A transaction is a group of one or more database statements that are either wholly committed or wholly rolled back.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: 05/03/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: language-reference
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azure-sqldw-latest || = fabric"
---
# Transactions (Azure Synapse Analytics and Microsoft Fabric)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw-fabricdw.md)]

  A transaction is a group of one or more database statements that are either wholly committed or wholly rolled back. Each transaction is atomic, consistent, isolated, and durable (ACID). If the transaction succeeds, all statements within it are committed. If the transaction fails, that is at least one of the statements in the group fails, then the entire group is rolled back.  
  
 The beginning and end of transactions depends on the AUTOCOMMIT setting and the BEGIN TRANSACTION, COMMIT, and ROLLBACK statements. 

 The following types of transactions are supported:  
  
-   *Explicit transactions* start with the BEGIN TRANSACTION statement and end with the COMMIT or ROLLBACK statement.  
  
-   *Auto-commit transactions* initiate automatically within a session and do not start with the BEGIN TRANSACTION statement. When the AUTOCOMMIT setting is ON, each statement runs in a transaction and no explicit COMMIT or ROLLBACK is necessary. When the AUTOCOMMIT setting is OFF, a COMMIT or ROLLBACK statement is required to determine the outcome of the transaction. Autocommit transactions begin immediately after a COMMIT or ROLLBACK statement, or after a SET AUTOCOMMIT OFF statement.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range="=fabric"

> [!NOTE]
> For more information on transactions in [!INCLUDE [fabric](../../includes/fabric.md)], see [Transactions in [!INCLUDE [fabric](../../includes/fabric.md)]](/fabric/data-warehouse/transactions).

::: moniker-end
  
## Syntax  
  
```syntaxsql
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## Arguments  
 BEGIN TRANSACTION  
 Marks the starting point of an explicit transaction.  
  
 COMMIT [ WORK ]  
 Marks the end of an explicit or autocommit transaction. This statement causes the changes in the transaction to be permanently committed to the database. The statement COMMIT is identical to COMMIT WORK, COMMIT TRAN, and COMMIT TRANSACTION.  
  
 ROLLBACK [ WORK ]  
 Rolls back a transaction to the beginning of the transaction. No changes for the transaction are committed to the database. The statement ROLLBACK is identical to ROLLBACK WORK, ROLLBACK TRAN, and ROLLBACK TRANSACTION.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 Determines how transactions can start and end.  
  
 ON  
 Each statement runs under its own transaction and no explicit COMMIT or ROLLBACK statement is necessary. Explicit transactions are allowed when AUTOCOMMIT is ON.  
  
 OFF  
 [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE [fabric](../../includes/fabric.md)] automatically initiates a transaction when a transaction is not already in progress. Any subsequent statements are run as part of the transaction and a COMMIT or ROLLBACK is necessary to determine the outcome of the transaction. As soon as a transaction commits or rolls back under this mode of operation, the mode remains OFF, a new transaction is initiated. Explicit transactions are not allowed when AUTOCOMMIT is OFF.  
  
 If you change the AUTOCOMMIT setting within an active transaction, the setting does affect the current transaction and does not take affect until the transaction is completed.  
  
 If AUTOCOMMIT is ON, running another SET AUTOCOMMIT ON statement has no effect. Likewise, if AUTOCOMMIT is OFF, running another SET AUTOCOMMIT OFF has no effect.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 This toggles the same modes as SET AUTOCOMMIT. When ON, SET IMPLICIT_TRANSACTIONS sets the connection into implicit transaction mode. When OFF, it returns the connection to autocommit mode.  For more information, see [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## Permissions  
 No specific permissions are required to run the transaction-related statements. Permissions are required to run the statements within the transaction.  
  
## Error Handling  
 If COMMIT or ROLLBACK are run and there is no active transaction, an error is raised.  
  
 If a BEGIN TRANSACTION is run while a transaction is already in progress, an error is raised. This can occur if a BEGIN TRANSACTION occurs after a successful BEGIN TRANSACTION statement or when the session is under SET AUTOCOMMIT OFF.  
  
 If an error other than a run-time statement error prevents the successful completion of an explicit transaction, the daabase engine automatically rolls back the transaction and frees all resources held by the transaction. For example, if the client's network connection is broken or the client logs off the application, any uncommitted transactions for the connection are rolled back when the network notifies the instance of the break.  
  
 If a run-time statement error occurs in a batch, [!INCLUDE [ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE [fabric](../../includes/fabric.md)] behave consistent with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT** set to **ON** and the entire transaction is rolled back. For more information about the **XACT_ABORT** setting, see [SET XACT_ABORT (Transact-SQL)](../statements/set-xact-abort-transact-sql.md).  
  
## General Remarks  
 A session can only run one transaction at a given time; save points and nested transactions are not supported.  
  
 It is the responsibility of the programmer to issue COMMIT only at a point when all data referenced by the transaction is logically correct.  
  
 When a session is terminated before a transaction completes, the transaction is rolled back.  
  
 Transaction modes are managed at the session level. For example, if one session begins an explicit transaction or sets AUTOCOMMIT to OFF, or sets IMPLICIT_TRANSACTIONS to ON, it has no effect on the transaction modes of any other session.  
  
## Limitations and Restrictions  
 You cannot roll back a transaction after a COMMIT statement is issued because the data modifications have been made a permanent part of the database.  
  
 The [CREATE DATABASE &#40;Azure Synapse Analytics&#41;](../statements/create-database-transact-sql.md) and [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) commands cannot be used inside an explicit transaction.  
  
 [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE [fabric](../../includes/fabric.md)] do not have a transaction sharing mechanism. This implies that at any given point in time, only one session can be doing work on any transaction in the system.  
  
## Locking Behavior  
 Locking ensures the integrity of transactions and maintain the consistency of databases when multiple users are accessing data at the same time. Locking is used by both implicit and explicit transactions. Each transaction requests locks of different types on the resources, such as tables or databases on which the transaction depends. 

All locks are table level or higher. The locks block other transactions from modifying the resources in a way that would cause problems for the transaction requesting the lock. Each transaction frees its locks when it no longer has a dependency on the locked resources; explicit transactions retain locks until the transaction completes when it is either committed or rolled back.  
  
## Examples: 
  
### A. Using an explicit transaction  
  
```sql  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### B. Rolling back a transaction  
 The following example shows the effect of rolling back a transaction.  In this example, the ROLLBACK statement will roll back the INSERT statement, but the created table will still exist.  
  
```sql  
CREATE TABLE ValueTable (id INT);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### C. Setting AUTOCOMMIT  
 The following example sets the AUTOCOMMIT setting to `ON`.  
  
```sql  
SET AUTOCOMMIT ON;  
```  
  
 The following example sets the AUTOCOMMIT setting to `OFF`.  
  
```sql  
SET AUTOCOMMIT OFF;  
```  
  
### D. Using an implicit multi-statement transaction  
  
```sql  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id INT);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## Next steps

- [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
- [Transactions, inserting and modifying data in Microsoft Fabric Warehouse](/fabric/data-warehouse/transactions)