---
title: "Create and Modify Embedded Data Sources"
description: Learn how to create and modify embedded data sources that are defined in a report definition and only used by that report.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-data
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Create and Modify Embedded Data Sources
  An embedded data source is defined in a report definition and used only by that report.  
  
## To create an embedded data source in Report Designer  
  
1.  On the toolbar in the Report Data pane, click **New** and then click **Data Source**. The **Data Source Properties** dialog box opens.  
  
    > [!NOTE]  
    >  If the Report Data pane is not visible, click **Report Data** on the **View** menu.  
  
2.  In the **Name** text box, type a name for the data source or accept the default. The data source name is used internally within the report. For clarity, we recommend that the name of the data source contain the name of the database specified in the connection string.  
  
3.  Verify that **Embedded connection** is selected, and do the following.  
  
    1.  From the **Type** drop-down list, select a data source type; for example, **Microsoft SQL Server** or **OLE DB**.  
  
    2.  Specify a connection string using one of the following alternatives:  
  
        -   Type the connection string directly in the **Connection string** text box. For a list of example connection strings, see [Create data connection strings - Report Builder & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Click the expression (**fx**) button to create an expression that evaluates to a connection string. In the **Expression** dialog box, type the expression in the Expression pane. Select **OK**.
  
        -   Click **Edit** to open the **Connection Properties** dialog box for the data source type you chose in step 2.  
  
             Fill in the fields in the **Connection Properties** dialog box as appropriate for the data source type. Connection properties include the type of data source, the name of the data source, and the credentials to use. After you specify values in this dialog box, click **Test Connection** to verify that the data source is available and that the credentials you specified are correct. For more information about specific data source types, see topics in [Add Data from External Data Sources &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
    3.  Click **Credentials**.  
  
         Specify the credentials to use for this data source. The owner of the data source chooses the type of credentials that are supported.  
  
4.  The new embedded data source appears in the Report Data pane.  
  
## To create an embedded data source in Report Builder  
  
1.  On the toolbar in the Report Data pane, click **New**, and then click **Data Source**. The **Data Source Properties** dialog box opens.  
  
2.  In the **Name** text box, type a name for the data source or accept the default.  
  
3.  Verify that **Use a connection embedded in my report** is selected.  
  
    1.  From the **Select connection type** drop-down list, select a data source type; for example, **Microsoft SQL Server** or **OLE DB**.  
  
    2.  Specify a connection string by using one of the following alternatives:  
  
        -   Type the connection string directly in the **Connection string** text box. For a list of example connection strings, see [Create data connection strings - Report Builder & SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Click the expression (**fx**) button to create an expression that evaluates to a connection string. In the **Expression** dialog box, type the expression in the Expression pane. Select **OK**.
  
        -   Click **Build** to open the **Connection Properties** dialog box for the data source type that you chose in step 2.  
  
             Fill in the fields in the **Connection Properties** dialog box as appropriate for the data source type. Connection properties include the type of data source, the name of the data source, and the credentials to use. After you specify values in this dialog box, click **Test Connection** to verify that the data source is available and that the credentials you specified are correct.  
  
4.  Click **Credentials**.  
  
     Specify the credentials to use for this data source. The owner of the data source chooses the type of credentials that are supported. For more information, see [Specify Credential and Connection Information for Report Data Sources](specify-credential-and-connection-information-for-report-data-sources.md).  
  
5.  Select **OK**.
  
     The data source appears in the Report Data pane.  
  
## See Also  
 [Report Embedded Datasets and Shared Datasets &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Specify Credential and Connection Information for Report Data Sources](specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
