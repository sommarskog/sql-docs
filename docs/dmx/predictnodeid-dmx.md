---
title: "PredictNodeId (DMX)"
description: "PredictNodeId (DMX)"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: dmx
---
# PredictNodeId (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Returns the Node_ID of the node to which the case is classified.  
  
## Syntax  
  
```  
  
PredictNodeId(<scalar column reference>)  
```  
  
## Applies To  
 A scalar column.  
  
## Return Type  
 \<scalar expression>  
  
## Examples  
 The following example returns whether the specified individual is likely to buy a bicycle, and also returns the nodeID of the node that they are most likely to be part of.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictNodeId([Bike Buyer])  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 You could then use the following statement to determine what is contained within the node:  
  
```  
SELECT   
  NODE_CAPTION   
FROM   
  [TM Decision Tree].CONTENT  
WHERE NODE_UNIQUE_NAME= '00000000100'   
```  
  
## See Also  
 [Data Mining Extensions &#40;DMX&#41; Function Reference](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Functions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [General Prediction Functions &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
