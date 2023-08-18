---
title: "Add and Verify a Data Connection (Report Builder)"
description: Learn how to use Report Builder to add and verify a data connection to verify that the credentials that are specified are sufficient.
author: maggiesMSFT
ms.author: maggies
ms.date: 12/13/2020
ms.service: reporting-services
ms.subservice: report-data
ms.topic: conceptual
ms.custom: updatefrequency5
---

# Add and Verify a Data Connection (Report Builder and SSRS)

In Report Builder, you can add a shared data source from the report server or create an embedded data source for your report. In Report Designer, you can create a shared data source or an embedded data source and deploy it to a report server.

To add a shared data source to your report, browse to a report server and select a shared data source. The shared data source in your report points to the shared data source definition on the report server.

To create an embedded data source, you must have connection information to the external source of data and you must know which permissions you need to access the data. This information usually comes from the owner of the data source. You can test the connection to verify that the credentials that are specified are sufficient.

For more information, see [Create data connection strings - Report Builder & SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) and [Specify Credentials in Report Builder](./specify-credential-and-connection-information-for-report-data-sources.md)

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## To create a connection to a shared data source in Report Builder

1. On the toolbar in the Report Data pane, click **New,** and then click **Data Source**. The **Data Source Properties** dialog box opens.

2. In the **Name** text box, type a name for the data source.

    > [!NOTE]  
    >  This name is saved in the local report definition. This name is not the name of the shared data source on the report server. 

3. Select **Use a shared connection or report model**. The list of recently used shared data sources and report models appears. To select one from a report server, click **Browse** and browse to the folder on the report server where shared data sources are available.

4. Select the shared data source and then click **Open**.

5. Select **OK**.

The data source appears in the Report Data pane.

### To verify a data connection  

1. On the toolbar in the Report Data pane, double-click the data source. The **Data Source Properties** dialog box opens.

2. Click **Test Connection**.

3. If the connection is successful, the following message appears: "Connection created successfully". Select **OK**.

4. If the connection is not successful, the following message appears: "Unable to connect to the data source."  

5. Click **Details**, and use the information to correct the issue.

    For more information, see [Specify Credentials in Report Builder](./specify-credential-and-connection-information-for-report-data-sources.md).

6. Select **OK**.

## See also

- [Report Datasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
- [Report Embedded Datasets and Shared Datasets &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)
- [Finding, Viewing, and Managing Reports &#40;Report Builder and SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
- [Create data connection strings - Report Builder & SSRS](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
