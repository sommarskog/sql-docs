---
title: "Change Time Zones and Clock Settings on a Report Server"
description: Change time zones & clock settings for a report server. You can't set a report server time zone, so set the computer's time zone or SharePoint region settings.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: subscriptions
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "time zones [Reporting Services]"
  - "clocks [Reporting Services]"
  - "schedules [Reporting Services], clock settings"
  - "schedules [Reporting Services], time zones"
---
# Change Time Zones and Clock Settings on a Report Server
  A report server always uses the local time of the computer on which it is installed. You cannot configure it to use a different time zone. If a client application points to a report server in a different time zone, the report server time zone is used to execute a scheduled operation. In Report Manager and SharePoint management pages, the time zone is indicated on each scheduling page so that you know exactly when a scheduled operation will occur. For example, the page for creating custom schedules will note "Times are expressed in (UTC-08:00) Pacific time (US and Canada)."
  The report server creates a SQL Server Agent job that is used to trigger the schedule. When the Report Server and the SQL Server Agent are located on separate servers, the time zone must be the same on all servers.
  
## Changing the Time Zone (Native Mode)  
 If you change the time zone on a computer hosting a report server, you must restart the Report Server service in order for the time zone change to take effect.  
  
 Timestamp values of existing report history snapshots are synchronized to the new time zone setting. If you generated a report history snapshot at 9:00 A.M., and then reset the time zone ahead one time zone, the timestamp on the generated snapshot will change from 9:00 A.M. to 10:00 A.M.  
  
 Schedules retain existing settings, except that they are mapped to the new time zone. For example, if a schedule runs at 2:00 A.M. Pacific Standard Time and you change the time zone to East Australia Standard Time, the schedule runs at 2:00 A.M. East Australia Standard Time.  
  
 Property timestamp values (for example, the time at which a folder or linked report item is created) are not synchronized to a new time zone setting. If you create an item on June 25 at 9:00 A.M., and then reset the time zone or clock, the timestamp remains June 25 at 9:00 A.M.  
  
## Changing the Time Zone (SharePoint Mode)  
 The time zone configuration for [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode is managed as part of the SharePoint regional settings. For more information, see [Regional settings (SharePoint Server 2010 (/previous-versions/office/sharepoint-server-2010/cc824907(v=office.14))](/previous-versions/office/sharepoint-server-2010/cc824907(v=office.14)).  
  
## Changing the Clock Settings  
 Changing the computer clock has no effect on existing timestamp values (for example, if you move the clock forward an hour, the timestamps of report history snapshots do not change). There may be a delay of 10 seconds before the Scheduling and Delivery Processor uses the new setting. The actual delay may vary if you modified polling interval settings in the configuration files.  
  
## See Also  
 [Start and Stop the Report Server Service](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [Schedules](../../reporting-services/subscriptions/schedules.md)  
  
