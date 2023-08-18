---
title: "Step 4: Test the Lesson 2 tutorial package"
description: "Lesson 2-4: Test the Lesson 2 tutorial package"
author: chugugrace
ms.author: chugu
ms.date: "01/03/2019"
ms.service: sql
ms.subservice: integration-services
ms.topic: tutorial
---
# Lesson 2-4: Test the Lesson 2 tutorial package

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



With the Foreach Loop container and the Flat File connection manager now configured, the Lesson 2 package can iterate through the 14 flat files in the Sample Data folder. Each time a file name matches the specified criterion, the Foreach Loop container populates the user-defined variable with the file name. This variable, in turn, updates the ConnectionString property of the Flat File connection manager, which connects to that flat file. The Foreach Loop container then runs the unmodified data flow task against the data in that flat file.  
  
> [!NOTE]  
> If you ran the package from Lesson 1, you need to delete the records from the dbo.NewFactCurrencyRate table in the [!INCLUDE [sssampledbdwobject-md](../includes/sssampledbdwobject-md.md)] database before you run the package from this lesson. Lesson 2 attempts to insert records already inserted in Lesson 1, which causes an error.  
  
## Check the package layout  
Before you test the package, verify that the control and data flows in the Lesson 2 package contains the objects shown in the following diagrams. Lesson 2's data flow is the same as Lesson 1.  
  
**Control Flow**  
  
![Control flow in package](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Data Flow**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## Test the Lesson 2 tutorial package  
  
1.  In **Solution Explorer**, right-click **Lesson 2.dtsx** and select **Execute Package**.  
  
    The package runs. You can verify the status of each loop in the **Output** window, or by selecting the **Progress** tab. For example, you can see that 1,097 rows were added to the destination table from the file Currency_VEB.txt.  
  
2.  After the package has completed running, on the **Debug** menu, select **Stop Debugging**.  
  
## Go to next lesson  
[Lesson 3: Add logging with SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## See also  
[Execution of projects and packages](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

