---
title: Match Similar Data
description: "Match Similar Data (MDS Add-in for Excel)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
ms.custom: microsoft-excel-add-in
---
# Match Similar Data (MDS Add-in for Excel)

[!INCLUDE [SQL Server Windows Only - ASDBMI](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In the [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use Data Quality Services (DQS) functionality to find similarities in your data.  
  
 To perform this procedure, you can:  
  
-   Use the default Data Quality Services knowledge base, or  
  
-   Create your own custom DQS knowledge base and matching policy. For more information, see [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md).  
  
## Prerequisites  
  
-   You must have a worksheet that contains MDS-managed data. For more information, see [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
-   Optional. You can combine other data with the MDS-managed data before checking for similarities. For more information, see [Combine Data &#40;MDS Add-in for Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md).  
  
### To find similarities by using the default knowledge base  
  
1.  From the worksheet that contains MDS-managed data, in the **Data Quality** group, click **Match Data**.  
  
2.  In the **Match Data** dialog box, from the **DQS Knowledge Base** list, select **DQS Data (default)**.  
  
3.  For each column that contains data you want to match, add a row in the dialog box. For information about the fields in this dialog box, see [How to Set Matching Rule Parameters](../../data-quality-services/create-a-matching-policy.md#MatchingRules).  
  
4.  When the total of all weight values equals 100 percent, click **OK**.  
  
### To find similarities by using a custom knowledge base  
  
1.  From the worksheet that contains MDS-managed data, in the **Data Quality** group, click **Match Data**.  
  
2.  From the **DQS Knowledge Base** list, select the name of your custom knowledge base.  
  
3.  For each column in the worksheet, select a DQS domain.  
  
4.  When all DQS domains are mapped to columns in the worksheet, click **OK**.  
  
## Next Steps  
  
-   View additional information to determine which data is similar. For more information, see [Data Quality Matching Columns &#40;MDS Add-in for Excel&#41;](../../master-data-services/microsoft-excel-add-in/data-quality-matching-columns-mds-add-in-for-excel.md).  
  
## See Also  
 [Data Quality Matching in the MDS Add-in for Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Data Matching](../../data-quality-services/data-matching.md)  
  
  
