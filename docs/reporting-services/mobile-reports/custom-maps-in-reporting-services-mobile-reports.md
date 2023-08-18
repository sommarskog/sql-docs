---
title: "Custom maps in Reporting Services mobile reports"
description: Learn about geographic maps in SQL Server Mobile Report Publisher, defined in a format known as ESRI shapefiles.
author: maggiesMSFT
ms.author: maggies
ms.date: 07/21/2022
ms.service: reporting-services
ms.subservice: mobile-reports
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Custom maps in Reporting Services mobile reports

[!INCLUDE [ssrs-mobile-report-deprecated](../../includes/ssrs-mobile-report-deprecated.md)]

Geographic maps in SQL Server Mobile Report Publisher are defined in a format known as *ESRI shapefiles*.  
  
Initially designed by a private company, this is now a widespread semi-open format used in a large portion of GIS applications. In accordance with this format, Mobile Report Publisher requires two files to be provided when defining a map:  
  
- A .SHP file for shape geometries  
- A .DBF file for metadata  
  
The base files names must match (e.g. *canada.shp* and *canada.dbf*). The metadata must include the field *NAME* with the value of the corresponding shape's name (key), to be used when populating the map with data.  

The two map files together, the SHP and the DBF, can be no bigger than 512 KB. If your map files are too big, use a tool like [https://mapshaper.org/](https://mapshaper.org/) to reduce their size.  
  
See how to [add custom maps to mobile reports](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## Technical information  
  
- The official specification: [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- The Wikipedia shapefile article: [https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## Creating & editing map geometry  
  
Creating and editing shapefiles is a complex process that is beyond the scope of this document. Here are some resources and applications to help you get started:  
  
- ArcGIS: [https://www.arcgis.com/](https://www.arcgis.com/)  
- MAPublisher plug-in for Adobe Illustrator: [https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS (free): [https://www.qgis.org/](https://www.qgis.org/)  

## Existing shapefiles  
  
Many existing shapefiles can be downloaded from the Web, from sites like Diva-GIS: [https://www.diva-gis.org/Data](https://www.diva-gis.org/Data).  

## See also  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
