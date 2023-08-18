---
title: "Add a multi-value parameter to a paginated report"
description: Learn how to add a parameter to a paginated report that allows the user to select more than one value for the parameter in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/07/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Add a multi-value parameter to a paginated report

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  You can add a parameter to a paginated report that allows the user to select more than one value for the parameter.  
  
 You can pass multiple parameter values to the report within the report URL. For a URL example includes a multi-value parameter, see [Pass a Report Parameter Within a URL](../../reporting-services/pass-a-report-parameter-within-a-url.md).  
  
 For information on how to pass multiple parameter values to a stored procedure, see [Working With Multi-Select Parameters for SSRS Reports](https://go.microsoft.com/fwlink/?LinkId=321529) on mssqltips.com.  
  
## To add a multi-value parameter  
  
1.  In Report Builder, open the report that you want to add the multi-value parameter to.  
  
2.  Right-click the report dataset, and then click **Dataset Properties**  
  
3.  Add a variable to the dataset query by either editing the query text in the **Query** box, or by adding a filter by using the query designer. For more information, see [Build a Query in the Relational Query Designer &#40;Report Builder and SSRS&#41;](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    > *  The query text must not include the DECLARE statement for the query variable.  
    > *  The text for the query variable must include the **IN** operator, as shown in the example above.  
    > *  Be sure to include the parentheses around the variable as shown above. Otherwise, the report fails to render and the "must declare the scalar variable" error is displayed.  
  
    A dataset parameter for an embedded dataset or a shared dataset is created automatically for the query variable. A report parameter is created automatically for the dataset parameter.  
  
4.  In the **Report Data** pane, expand the **Parameters** node, right-click the report parameter that was automatically created for the dataset parameter, and then click **Parameter Properties**.  
  
5.  In the **General** tab, select **Allow multiple values** to allow a user to select more than one value for the parameter.  
  
6.  (Optionally) In the **Available** values tab, specify a list of available values to display to the user.  
  
     An available values list limits the choices a user can make to only valid values for the parameter. For multiple values, the top of list begins with a **Select All** feature so the user can select or clear all values with a single click. If you choose to get the available values for the report parameter from a dataset query, be sure to select a dataset that does not contain the query variable that is associated with the same report parameter.  
  
     For more information, see [Add, Change, or Delete Available Values for a Report Parameter &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  

## See Also  
 [Add Cascading Parameters to a Report &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Add, Change, or Delete a Report Parameter &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  
