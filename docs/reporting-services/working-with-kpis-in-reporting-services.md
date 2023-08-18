---
title: Working with KPIs in Reporting Services
description: Learn how you can easily measure status and performance by using KPIs in SQL Server Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.date: 01/06/2022
ms.service: reporting-services
ms.subservice: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
---

# Working with KPIs in Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

A *Key Performance Indicator (KPI)* is a visual cue that communicates the amount of progress made toward a goal.  Key Performance Indicators are valuable for teams, managers, and businesses to evaluate quickly the progress made against measurable goals.
  
By using KPIs in Power BI Report Server or SQL Server Reporting Services, you can easily visualize answers to the following questions:  
  
- What am I ahead or behind on?  
- How far ahead or behind am I?  
- What are the minimum amounts I have completed?  

> [!NOTE]
> KPIs are only accessible in Power BI Report Server and the Enterprise (Developer) editions of the Reporting Services portal.

## Create a dataset

A KPI will only use the first row of data from a shared dataset. Make sure that the data you want to use is located on that first row. To create a shared dataset, you can use either Report Builder or SQL Server Data Tools.  
  
> **Note**: The Dataset does not need to be in the same folder as the KPI.  
  
## Placement of KPIs  
  
KPIs can be created in any folder in your report server.  Before you create a KPI, you will want to think about where is the right location to place it in. You can place it in a folder that is visible to the users, at the same time being relevant to other reports, and KPIs, around it.  

## Add a KPI
  
After you have determined the location of your KPI, go to that folder and select **New** > **KPI** from the top menu.  
  
![Screenshot Showing the New dropdown list with the KPI option called out.](../reporting-services/media/rscreatekpi1.png)  
  
The **New KPI** screen opens.  
  
![Screenshot showing the New KPI screen.](../reporting-services/media/rscreatekpi2.png)  
  
You can either assign static values, or use data from a shared dataset. When you create a new KPI, it will be populated with a random set of manual data.  
  
| Field | Description |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Value format | Used to change the format of the value being displayed. |
| Value | The value to display for the KPI. |
| Goal | Used as a comparison to a numeric value and shown as a percent difference. |
| Status | Numerical value used to determine the KPI Tile color. Valid values are 1 (green), 0 (amber) and -1 (red). |
| Trend set | Comma-separated numeric values used for chart visualization. It can also be set to a column of a dataset with values that represent the trend. |
| Related content | The ability to set a drill-through link. This link can either be a mobile report published on the portal or a custom URL. |
  
> **Warning**: While you can use the word value for the **Status** field at design time, you should use the number value if refreshing a dataset. If you refresh a dataset with the word value, instead of the number, it could corrupt the KPIs on your server.  
>
> **Note**: The **Value**, **Goal** and **Status** fields can only choose a value from the first row of a dataset's result. The **Trend set** field, however, can choose which column reflects the trend.  
  
To use data from a shared dataset, you can do the following steps.
  
1. Change the fields drop down box from **Set manually**, or **Not set**, to **Dataset field**.  
  
    ![Screenshot showing the Value option set to Dataset field and the Pick dataset field set to Not set.](../reporting-services/media/rscreatekpi3.png)  
  
2. Select **More options (...)** in the data box to open the **Pick a Dataset** screen.  
  
    ![Screenshot of the Pick a Dataset section with the Finance_KPI option being selected.](../reporting-services/media/rscreatekpi4.png)  
  
3. Select the dataset that has the data you want to display.  
  
4. Choose the field you want to use. Select **OK**.  
  
    ![Screenshot showing the Pick a Field from Finance_KPI section with the Sum_Amount option being selected.](../reporting-services/media/rscreatekpi5.png)  
  
5. Change **Value format** to match the format of your value. In this example, the value is a currency.  
  
    ![Screenshot of the KPI preview showing the Value format option set to Currency.](../reporting-services/media/rscreatekpi6.png)  
  
6. Select **Apply**.  
  
    ![Screenshot of the KPIs showing that the Datasets has two items.](../reporting-services/media/rscreatekpi7.png)

## Configure related content

When you choose **Mobile Report**, you can choose the destination in a dialog.

   ![Screenshot showing the Related content option set to Mobile report and the Choose a mobile report option set to Not set.](media/rscreatekpi-related-content-mobile-report.png)

When you now click on the KPI in the portal, a thumbnail of the mobile report shows under the related content dropdown. Clicking on this thumbnail can directly navigate you to this report.

You can also specify a custom URL. This task can be anything: a website, a SharePoint site, a URL to an SSRS report (which would allow you to pass along hardcoded parameters).

![Screenshot showing the Related content option set to Custom URL and the Enter a URL option set to http://.](media/rscreatekpi-related-content-custom-url.png)

When you now click on the KPI, the URL shows under related content.

It's only possible to add one mobile report or one custom URL.
 
## Set up a cache refresh plan for a KPI  
  
You need to set up a cache refresh plan for the shared dataset that your KPI is based on. Otherwise, the KPI data won't refresh. The [Caching section](../reporting-services/work-with-shared-datasets-web-portal.md#caching) of the *Work with Shared Datasets* article explains how to set up cache refresh plans.  

## Remove a KPI  
  
To remove a KPI, you can do the following steps.
  
1. Select the **ellipsis (...)** of the KPI you want to remove. Select **Manage**.  
  
    ![Screenshot of the ellipsis option for a KPI selected and the MANAGE option called out.](../reporting-services/media/rsremovekpi1.png)  
  
2. Select **Delete**. Select **Delete** again on the confirmation dialog.  
  
    ![Screenshot of the Delete option.](../reporting-services/media/rsremovekpi2.png)  
  
 
## Next steps
  
[Web portal](../reporting-services/web-portal-ssrs-native-mode.md)  
[Work with Shared Datasets](../reporting-services/work-with-shared-datasets-web-portal.md)

More questions? [Try asking the Reporting Services forum](/answers/search.html?c=&f=&includeChildren=&q=ssrs+OR+reporting+services&redirect=search%2fsearch&sort=relevance&type=question+OR+idea+OR+kbentry+OR+answer+OR+topic+OR+user)
