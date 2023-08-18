---
title: "Step 7: Add and configure the OLE DB destination"
description: "Lesson 1-7: Add and configure the OLE DB destination"
author: chugugrace
ms.author: chugu
ms.date: "01/03/2019"
ms.service: sql
ms.subservice: integration-services
ms.topic: tutorial
---
# Lesson 1-7: Add and configure the OLE DB destination

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Your package can now extract data from the flat file source and transform that data into a format compatible with the destination. The next task is to load the transformed data into the destination. To load the data, you add an OLE DB destination to the data flow. The OLE DB destination can use a database table, view, or a SQL command to load data into a variety of OLE DB-compliant databases.  
  
In this task, you add and configure an OLE DB destination to use the OLE DB connection manager that you previously created.  
  
## Add and configure the sample OLE DB destination  
  
1.  In the **SSIS Toolbox**, expand **Other Destinations**, and drag **OLE DB Destination** onto the design surface of the **Data Flow** tab. Place the **OLE DB Destination** directly below the **Lookup Date Key** transformation.  
  
2.  Select the **Lookup Date Key** transformation and drag its blue arrow over to the new **OLE DB Destination** to connect the two components together.  
  
3.  In the **Input Output Selection** dialog, in the **Output** list box, select **Lookup Match Output**, and then select **OK**.  
  
4.  On the **Data Flow** design surface, select the name **OLE DB Destination** in the new **OLE DB Destination** component, and change that name to **Sample OLE DB Destination**.  
  
5.  Double-click **Sample OLE DB Destination**.  
  
6.  In the **OLE DB Destination Editor** dialog, ensure that **localhost.AdventureWorksDW2022** is selected in the **OLE DB Connection manager** box.  
  
7.  In the **Name of the table or the view** box, enter or select **[dbo].[FactCurrencyRate]**.  
 
8.  If a table named **NewFactCurrencyRate** currently exists, delete it now. You will create the table in the next step.
 
9.  Select the **New** button to create a new table.  Change the name of the table in the script from **Sample OLE DB Destination** to **NewFactCurrencyRate**.  Select **OK**.  
 
10. Upon selecting **OK**, the dialog closes and the **Name of the table or the view** automatically changes to **NewFactCurrencyRate**.  
  
11. Select **Mappings**.  
  
12. Verify that the **AverageRate**, **CurrencyKey**, **EndOfDayRate**, and **DateKey** input columns are mapped correctly to the destination columns. If same-named columns are mapped, the mapping is correct.  
  
13. Select **OK**.  
  
14. Right-click the **Sample OLE DB Destination** destination and select **Properties**.  
  
15. In the **Properties** window, verify that the **LocaleID** property is set to **English (United States)** and the **DefaultCodePage** property is set to **1252**.  
  
## Go to next task
[Step 8: Annotate and format the Lesson 1 package](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## See also  
[OLE DB destination](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
