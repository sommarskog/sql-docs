---
title: "Identity and Access Control (Replication)"
description: "Identity and Access Control (Replication)"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "11/20/2018"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "access controls [SQL Server replication]"
  - "security [SQL Server replication], identity and access control"
  - "authentication [SQL Server replication]"
  - "identity [Replication]"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# Identity and Access Control (Replication)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Authentication is the process by which an entity (typically a computer in this context) verifies that another entity, also called a *principal*, (typically another computer or user) is who or what it claims to be. Authorization is the process by which an authenticated principal is given access to resources, such as a file in the file system, or a table in a database.  
  
 Replication security uses authentication and authorization to control access to replicated database objects and to the computers and agents involved in replication processing. This is accomplished through three mechanisms:  
  
-   Agent security  
  
     The replication agent security model allows fine-grained control over the accounts under which replication agents run and make connections. For detailed information about the agent security model, see [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). 
  
-   Administration roles  
  
     Ensure that the correct server and database roles are used for replication setup, maintenance, and processing. For more information, see [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   The publication access list (PAL)  
  
     Grant access to publications through the PAL. The PAL functions similarly to a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows access control list. When a Subscriber connects to the Publisher or Distributor and requests access to a publication, the authentication information passed by the agent is checked against the PAL. For more information and best practices for the PAL, see [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Filtering Published Data  
 In addition to using authentication and authorization to control access to replicated data and objects, replication includes two options to control what data is available at a Subscriber: column filtering and row filtering. For more information about filtering, see [Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 When you define an article, you can publish only those columns that are necessary for the publication, and omit those that are unnecessary or contain sensitive data. For example, when publishing the **Customer** table from the Adventure Works database to sales representatives in the field, you can omit the **AnnualSales** column, which might be relevant only to executives at the company.  
  
 Filtering published data allows you to restrict access to data and allows you to specify the data that is available at the Subscriber. For example, you can filter the **Customer** table so that corporate partners only receive information about those customers whose **ShareInfo** column has a value of "yes." For merge replication, there are security considerations if you use a parameterized filter that includes HOST_NAME(). For more, see the section "Filtering with HOST_NAME()" in [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  

## Manage Logins and Passwords in Replication
Specify the logins and passwords for replication agents when you configure replication. After configuring replication, you can change logins and passwords. For more information, see [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md). If you change the password for an account used by a replication agent, execute [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md).  

Support for the use of group Managed Service Accounts (gMSA) is introduced in SQL Server 2014. For more information, see the blog [Replication and group Managed Service Accounts](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/).
  
## See Also  
 [Threat and Vulnerability Mitigation &#40;Replication&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)
 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
