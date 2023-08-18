---
title: "Parameters collection references in a paginated report"
description: Discover how to use parameters in an expression to customize paginated report data and appearance based on user choices in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/07/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Built-in collections - Parameters collection references in a paginated report (Report Builder)


[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  Paginated report parameters are one of the built-in collections you can reference from an expression. By including parameters in an expression, you can customize report data and appearance based on choices a user makes. Expressions can be used for any report item property or text box property that provides the (*Fx*) or \<**Expression**> option. Expressions are also used to control report content and appearance in other ways. For more information, see [Expression Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
 When you compare parameter values with dataset field values at run time, the data types for the two items you are comparing must be the same. Report parameters can be one of the following types: Boolean, DateTime, Integer, Float, or Text, which represents the underlying data type String. If necessary, you might have to convert the data type of the parameter value to match the dataset value. For more information, see [Data Types in Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  
 In order to include a parameter reference in an expression, you must understand how to specify the correct syntax for the parameter reference, which varies depending on whether the parameter is a single-value or multivalue parameter.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> Using a Single-Valued Parameter in an Expression  
 The following table shows examples of the syntax to use when you include a reference to a single-value parameter of any data type in an expression.  
  
|Example|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<ParameterName>* `.IsMultiValue`|Returns **False**.<br /><br /> Checks if a parameter is multivalue. If **True**, the parameter is multivalue and it is a collection of objects. If **False**, the parameter is single-value and is a single object.|  
|`=Parameters!` *\<ParameterName>* `.Count`|Returns the integer value 1. For a single-value parameter, the count is always 1.|  
|`=Parameters!` *\<ParameterName>* `.Label`|Returns the parameter label, frequently used as the display name in a drop-down list of available values.|  
|`=Parameters!` *\<ParameterName>* `.Value`|Returns the parameter value. If the Label property has not been set, this value appears in the drop-down list of available values.|  
|`=CStr(Parameters!`  *\<ParameterName>* `.Value)`|Returns the parameter value as a string.|  
|`=Fields(Parameters!` *\<ParameterName>* `.Value).Value`|Returns the value for the field that has the same name as the parameter.|  
  
 For more information about using parameters in a filter, see [Add Dataset Filters, Data Region Filters, and Group Filters &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
##  <a name="Multi"></a> Using a Multivalue Parameter in an Expression  
 The following table shows examples of the syntax to use when you include a reference to a multivalue parameter of any data type in an expression.  
  
|Example|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<MultivalueParameterName>* `.IsMultiValue`|Returns **True** or **False**.<br /><br /> Checks if a parameter is multivalue. If **True**, the parameter is multivalue and is a collection of objects. If **False**, the parameter is single-valued and is a single object.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Count`|Returns an integer value.<br /><br /> Refers to the number of values. For a single-value parameter, the count is always 1. For a multivalue parameter, the count is 0 or more.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(0)`|Returns the first value in a multivalue parameter.|  
|`=Parameters!` *\<MultivalueParameterName>* `.Value(Parameters!` *\<MultivalueParameterName>* `.Count-1)`|Returns the last value in a multivalue parameter.|  
|`=Split("Value1,Value2,Value3",",")`|Returns an array of values.<br /><br /> Create an array of values for a multivalue **String** parameter. You can use any delimiter in the second parameter to Split. This expression can be used to set defaults for a multivalue parameter or to create a multivalue parameter to send to a subreport or drillthrough report.|  
|`=Join(Parameters!` *\<MultivalueParameterName>* `.Value,", ")`|Returns a **String** that consists of a comma-delimited list of values in a multivalue parameter. You can use any delimiter in the second parameter to Join.|  
  
 For more information about using parameters in a filter, see [Report Parameters &#40;Report Builder and Report Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## See Also  
 [Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Commonly Used Filters &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Add, Change, or Delete a Report Parameter &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Tutorial: Add a Parameter to Your Report &#40;Report Builder&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Report Builder Tutorials](../../reporting-services/report-builder-tutorials.md)   
 [Built-in Collections in Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)  
  
  
