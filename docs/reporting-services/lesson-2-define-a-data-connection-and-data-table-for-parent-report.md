---
title: "Lesson 2: Define a Data Connection and Data Table for Parent Report"
description: "Learn how to create a data connection and a data table for the parent report after you create a new website project using the ASP.NET website template for Visual C#."
author: maggiesMSFT
ms.author: maggies
ms.date: 05/18/2016
ms.service: reporting-services
ms.subservice: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Lesson 2: Define a Data Connection and Data Table for Parent Report
After you create a new website project using the ASP.NET website template for Visual C#, your next step is to create a data connection and a data table for the parent report.

[!INCLUDE [article-uses-adventureworks](../includes/article-uses-adventureworks.md)]
  
## To define a data connection and Data Table by adding a DataSet (for parent report)  
  
1.  On the **Website** menu, select **Add New Item**.  
  
2.  In the **Add New Item** dialog box, select **DataSet** and select **Add**. When prompted you should add the item to the **App_Code** folder by selecting **Yes**.  
  
    This adds a new XSD file **DataSet1.xsd** to the project and opens the DataSet Designer.  
  
3.  From the Toolbox window, drag a **[TableAdapter](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)** control to the design surface. This launches the **TableAdapter** Configuration Wizard.  
  
4.  On the **Choose Your Data Connection** page, select **New Connection**.  
  
5.  If this is the first time you've created a data source in Visual Studio, you will see the **Choose Data Source** page. In the **Data Source** box, select **Microsoft SQL Server**.  
  
6.  In the **Add Connection** dialog box, perform the following steps:  
  
    1.  In the **Server name** box, enter the server where the [!INCLUDE [sssampledbobject-md](../includes/sssampledbobject-md.md)] database is located.  
  
        The default SQL Server Express instance is **(local)\sqlexpress**.  
  
    2.  In the **Log on to the server** section, select the option that provides you access to the data. **Use Windows Authentication** is the default.  
  
    3.  From the **Select or enter a database name** drop-down list, select [!INCLUDE [sssampledbobject-md](../includes/sssampledbobject-md.md)].  
  
    4.  Select **OK**, and then select **Next**.  
  
7.  If you selected **Use SQL Server Authentication** in the Step 6 (b), select the option whether to include the sensitive data in the string or set the information in your application code.  
  
8.  On the **Save the Connection String to the Application Configuration File** page, type in the name for the connection string or accept the default **AdventureWorks2022ConnectionString**. Select **Next**.  
  
9. On the **Choose a Command Type** page, select **Use SQL Statements**, and then select **Next**.  
  
10. On the **Enter a SQL Statement** page, enter the following Transact-SQL query to retrieve data from the [!INCLUDE [sssampledbobject-md](../includes/sssampledbobject-md.md)] database, and then select **Next**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    You can also create the query by selecting **Query Builder**, and then verify the query by selecting **Execute Query**.
  
11. On the **Choose Methods to Generate** page, be sure to uncheck **Create methods to send updates directly to the database (GenerateDBDirectMethods)**, and then select **Finish**.  
  
    > [!WARNING]  
    > Be sure to uncheck **Create methods to send updates directly to the database (GenerateDBDirectMethods)**  
  
    You have now completed configuring the ADO.NET DataTable object as the data source for your report. On the DataSet Designer page in Visual Studio, you should see the DataTable object you added, listing the columns specified in the query. DataSet1 contains the data from the Product table, based on the query.  
  
12. Save the file.  
  
13. To preview the data, select **Preview Data** on the **Data** menu, and then select **Preview**.  
  
## Next Task  
You have successfully created a data connection and a data table for the parent report. Next, you will design the parent report using the Report Wizard. See [Lesson 3: Design the Parent Report using the Report Wizard](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md).  
  

