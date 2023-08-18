---
title: "View the Definition of a Stored Procedure"
description: Learn how to view the definition of procedure in Object Explorer and by using a system stored procedure, system function, and object catalog view in the Query Editor.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "08/19/2021"
ms.service: sql
ms.subservice: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
  - "stored procedures [SQL Server], viewing"
  - "definition of stored procedure"
  - "viewing stored procedures"
  - "displaying stored procedures"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# View the Definition of a Stored Procedure
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
    
##  <a name="Top"></a> View the definition of a stored procedure 

This article describes how to view the definition of procedure in Object Explorer and by using a system stored procedure, system function, and object catalog view in the Query Editor.  
  
-   **Before you begin:**  [Security](#Security)  
  
-   **To view the definition of a procedure, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 System Stored Procedure: **sp_helptext**  
 Requires membership in the **public** role. System object definitions are publicly visible. The definition of user objects is visible to the object owner or grantees that have any one of the following permissions: **ALTER**, **CONTROL**, **TAKE OWNERSHIP**, or **VIEW DEFINITION**.  
  
 System Function: **OBJECT_DEFINITION**  
 System object definitions are publicly visible. The definition of user objects is visible to the object owner or grantees that have any one of the following permissions: **ALTER**, **CONTROL**, **TAKE OWNERSHIP**, or **VIEW DEFINITION**. These permissions are implicitly held by members of the **db_owner**, **db_ddladmin**, and **db_securityadmin** fixed database roles.  
  
 Object Catalog View: **sys.sql_modules**  
 The visibility of the metadata in catalog views is limited to securables that a user either owns or on which the user has been granted some permission. For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

> [!NOTE]
> The system stored procedure `sp_helptext` is not supported in Azure Synapse Analytics. Instead, use `sys.sql_modules` object catalog view. Samples are provided later in this article.
  
##  <a name="Procedures"></a> How to View the Definition of a Stored Procedure  
 You can use one of the following:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
 **To view the definition a procedure in Object Explorer**  
  
1.  In Object Explorer, connect to an instance of [!INCLUDE[ssDE](../../includes/ssde-md.md)] and then expand that instance.  
  
2.  Expand **Databases**, expand the database in which the procedure belongs, and then expand **Programmability**.  
  
3.  Expand **Stored Procedures**, right-click the procedure and then select **Script Stored Procedure as**, and then select one of the following: **Create To**, **Alter To**, or **Drop and Create To**.  
  
4.  Select **New Query Editor Window**. This will display the procedure definition.  

###  <a name="TsqlProcedure"></a> Using Transact-SQL  

#### To view the definition of a procedure in Query Editor
  
 System Stored Procedure: **sp_helptext**  
 1.  In Object Explorer, connect to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  On the toolbar, select **New Query**.  
  
3.  In the query window, enter the following statement that uses the `sp_helptext` system stored procedure. Change the database name and stored procedure name to reference the database and stored procedure that you want.  
  
    ```sql  
    USE AdventureWorks2022;  
    GO  
    EXEC sp_helptext N'AdventureWorks2022.dbo.uspLogError';  
    ```  
  
#### System Function: **OBJECT_DEFINITION**  

 1.  In Object Explorer, connect to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  On the toolbar, select **New Query**.  
  
3.  In the query window, enter the following statements that use the `OBJECT_DEFINITION` system function. Change the database name and stored procedure name to reference the database and stored procedure that you want.  
  
    ```sql  
    USE AdventureWorks2022;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2022.dbo.uspLogError'));  
    ```  
  
#### <a id=sql_modules></a> Object Catalog View: **sys.sql_modules**  

 1.  In Object Explorer, connect to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  On the toolbar, select **New Query**.  
  
3.  In the query window, enter the following statements that use the `sys.sql_modules` catalog view. Change the database name and stored procedure name to reference the database and stored procedure that you want.  
  
    ```sql  
    USE AdventureWorks2022;  
    GO  
    SELECT [definition]
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'dbo.uspLogError'));  
    ```  
  
## See Also  
 [Create a Stored Procedure](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modify a Stored Procedure](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Delete a Stored Procedure](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [Rename a Stored Procedure](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  
