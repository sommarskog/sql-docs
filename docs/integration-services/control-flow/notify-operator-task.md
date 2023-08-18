---
title: "Notify Operator Task"
description: "Notify Operator Task"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.designer.notifyoperatortask.f1"
helpviewer_keywords:
  - "Notify Operator task"
  - "notifications [Integration Services]"
  - "SQL Server Agent [Integration Services]"
---
# Notify Operator Task

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  The Notify Operator task sends notification messages to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent operators. A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent operator is an alias for a person or group that can receive electronic notifications. For more information about [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operators, see [Operators](../../ssms/agent/operators.md).  
  
 By using the Notify Operator task, a package can notify one or more operators via e-mail, pager, or **net send**. Each operator can be notified by different methods. For example, OperatorA is notified by e-mail and pager, and OperatorB is notified by pager and **net send**. The operators who receive notifications from the task must be members of the **OperatorNotify** collection on the Notify Operator task.  
  
 The Notify Operator task is the only database maintenance task that does not encapsulate a Transact-SQL statement or a DBCC command.  
  
## Configuration of the Notify Operator Task  
 You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. This task is in the **Maintenance Plan Tasks** section of the **Toolbox** in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer.  
  
 For more information about the properties that you can set in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:  
  
-   [Notify Operator Task &#40;Maintenance Plan&#41;](../../relational-databases/maintenance-plans/notify-operator-task-maintenance-plan.md)  
  
 For more information about how to set these properties in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:  
  
-   [Set the Properties of a Task or Container](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
