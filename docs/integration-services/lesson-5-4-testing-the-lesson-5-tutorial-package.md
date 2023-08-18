---
title: "Step 4: Test the Lesson 5 package"
description: "Lesson 5-4: Test the Lesson 5 package"
author: chugugrace
ms.author: chugu
ms.date: "01/08/2019"
ms.service: sql
ms.subservice: integration-services
ms.topic: tutorial
---
# Lesson 5-4: Test the Lesson 5 package

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



At run time, your package obtains the value for the **Directory** property from a configuration variable, rather than from the directory name specified when you created the package. The value of the variable comes from the **SSISTutorial.dtsConfig** XML file.  
  
To verify that the package updates the **Directory** property with the new value during run time, run the package. Because only three sample data files are in the new directory, the data flow runs only three times.  
  
## Checking the Package Layout  
Before you test the package, verify that the control and data flows in the Lesson 5 package are similar to the objects shown in the following diagrams:  
  
**Control Flow**  
  
![Control flow in package](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Data Flow**  
  
![Data flow in package](../integration-services/media/task5lesson5data.gif "Data flow in package")
  
## Test the Lesson 5 package  
  
1.  On the **Debug** menu, select **Start Debugging**.  
  
2.  After the package has completed running, on the **Debug** menu, select **Stop Debugging**.  
  
## Next lesson  
[Lesson 6: Use parameters with the Project Deployment Model in SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
