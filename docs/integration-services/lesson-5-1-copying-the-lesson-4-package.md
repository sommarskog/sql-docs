---
title: "Step 1: Copy the Lesson 4 package"
description: "Lesson 5-1: Copy the Lesson 4 package"
author: chugugrace
ms.author: chugu
ms.date: "01/08/2019"
ms.service: sql
ms.subservice: integration-services
ms.topic: tutorial
---
# Lesson 5-1: Copy the Lesson 4 package

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



In this task, you create a copy of the **Lesson 4.dtsx** package from Lesson 4. If you did not complete lesson 4, you can add the completed lesson 4 package that is included with the tutorial to the project, and then make a copy of it to work with. You use this new copy throughout the rest of Lesson 5.  
  
## Create the Lesson 5 package  
  
Use this procedure if you're copying the completed Lesson 4.  To copy the sample Lesson 4, see the next section.

1.  If [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools isn't already open, select **Start** > **All Programs** > **Microsoft SQL Server 2017**, and then select **SQL Server Data Tools**.

2.  On the **File** menu, select **Open** > **Project/Solution**, select the **SSIS Tutorial** folder, and select **Open**.  Then, double-click **SSIS Tutorial.sln**.

3.  In **Solution Explorer**, right-click **Lesson 4.dtsx** and then select **Copy**.

4.  In **Solution Explorer**, right-click **SSIS Packages** and then select **Paste**.

    By default, the name of the copied package is **Lesson 5.dtsx**.

5.  In **Solution Explorer**, double-click **Lesson 5.dtsx** to open the package.

6.  Right-click anywhere in the background of the **Control Flow** design surface and select **Properties**.

7.  In the **Properties** window, change the **Name** property to **Lesson 5**.

8.  Select the box for the **ID** property, select the drop-down arrow, and then select **\<Generate New ID>**.

## Add the completed Lesson 4 package

1.  Open [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools and open the SSIS Tutorial project.

2.  In **Solution Explorer**, right-click **SSIS Packages** and select **Add Existing Package**.

3.  In the **Add Copy of Existing Package** dialog box, in **Package location**, select **File system**.

4.  Select the browse **(...)** button, navigate to **Lesson 4.dtsx** on your machine, and then select **Open**.

5.  Copy and paste the Lesson 4 package as described in steps 3-8 in the previous section.
  
## Go to next task  
[Step 2: Enable and configure package configurations](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
