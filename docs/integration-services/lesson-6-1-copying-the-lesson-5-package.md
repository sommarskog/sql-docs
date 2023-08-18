---
title: "Step 1: Copy the Lesson 5 package"
description: "Lesson 6-1: Copy the Lesson 5 package"
author: chugugrace
ms.author: chugu
ms.date: "01/11/2019"
ms.service: sql
ms.subservice: integration-services
ms.topic: tutorial
---
# Lesson 6-1: Copy the Lesson 5 package

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



In this task, you create a copy of the **Lesson 5.dtsx** package from Lesson 5. If you did not complete Lesson 5, you can add the completed Lesson 5 package included with the tutorial to the project, and then make a copy of it to work with. You use this new copy throughout the rest of Lesson 6. 

> [!IMPORTANT]
> After copying the Lesson 5 package, if you currently have the packages from the previous lessons in your solution, right-click each package from lessons 1-5 and select **Exclude From Project**. When done you should have only **Lesson 6.dtsx** in your solution.   
  
## Create the Lesson 6 package  
  
Use this procedure if you're copying the completed Lesson 5.  To copy the sample Lesson 5, see the next section.

1.  If [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools isn't already open, select **Start** > **All Programs** > **Microsoft SQL Server 2017**, and then select **SQL Server Data Tools**.

2.  On the **File** menu, select **Open** > **Project/Solution**, select the **SSIS Tutorial** folder and select **Open**, and then double-click **SSIS Tutorial.sln**.

3.  In **Solution Explorer**, right-click **Lesson 5.dtsx**, and then select **Copy**.

4.  In **Solution Explorer**, right-click **SSIS Packages**, and then select **Paste**.

    By default, the name of the copied package is **Lesson 6.dtsx**.

5.  In **Solution Explorer**, double-click **Lesson 6.dtsx** to open the package

6.  Right-click anywhere in the background of the **Control Flow** design surface and select **Properties**.

7.  In the **Properties** window, change the **Name** property to **Lesson 6**.

8.  Select the box for the **ID** property, select the drop-down arrow, and then select **\<Generate New ID>**.

## Add the completed Lesson 5 package

1.  Open [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools and open the SSIS Tutorial project.

2.  In **Solution Explorer**, right-click **SSIS Packages** and select **Add Existing Package**.

3.  In the **Add Copy of Existing Package** dialog box, in **Package location**, select **File system**.

4.  Select the browse **(...)** button, navigate to **Lesson 5.dtsx** on your machine, and then select **Open**.

5.  Copy and paste the Lesson 5 package as described in steps 3-8 in the previous section.

## Go to next task
[Step 2: Convert the project to the Project Deployment Model](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
