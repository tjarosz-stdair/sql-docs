---
description: "SP:CacheRemove Event Class"
title: "SP:CacheRemove Event Class | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: sql
ms.reviewer: ""
ms.technology: supportability
ms.topic: reference
helpviewer_keywords: 
  - "SP:CacheRemove event class"
ms.assetid: aaa3c5c4-2d3a-4832-a473-ce9bd4fb1c17
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# SP:CacheRemove Event Class
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  The SP:CacheRemove event class indicates that the stored procedure has been removed from the plan cache.  
  
## SP:CacheRemove Event Class Data Columns  
  
|Data column name|**Data type**|Description|Column ID|Filterable|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. This column is populated with the values passed by the application rather than the displayed name of the program.|10|Yes|  
|ClientProcessID|**int**|ID assigned by the host computer to the process where the client application is running. This data column is populated if the client provides the client process ID.|9|Yes|  
|DatabaseID|**int**|ID of the database in which the stored procedure is running. Determine the value for a database by using the DB_ID function.|3|Yes|  
|DatabaseName|**nvarchar**|Name of the database in which the stored procedure is running.|35|Yes|  
|EventClass|**int**|Type of event = 36.|27|No|  
|EventSequence|**int**|Sequence of a given event within the request.|51|No|  
|EventSubClass|**int**|Type of event subclass.<br /><br /> 1=Compplan Remove: A compiled query plan has been removed from the cache.<br /><br /> 2=Proc Cache Flush: All entries have been removed from the procedure cache.|21|Yes|  
|GroupID|**int**|ID of the workload group where the SQL Trace event fires.|66|Yes|  
|HostName|**nvarchar**|Name of the computer on which the client is running. This data column is populated if the client provides the host name. To determine the host name, use the HOST_NAME function.|8|Yes|  
|IsSystem|**int**|Indicates whether the event occurred on a system process or a user process. 1 = system, 0 = user.|60|Yes|  
|LoginName|**nvarchar**|Name of the login of the user (either [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows login credentials in the form of DOMAIN\username).|11|Yes|  
|LoginSid|**image**|Security identification number (SID) of the logged-in user. You can find this information in the sys.server_principals catalog view. Each SID is unique for each login in the server.|41|Yes|  
|NTDomainName|**nvarchar**|Windows domain to which the user belongs.|7|Yes|  
|NTUserName|**nvarchar**|Windows user name.|6|Yes|  
|ObjectID|**int**|System-assigned ID of the stored procedure.|22|Yes|  
|ObjectType|**int**|Value representing the type of the object involved in the event. This value corresponds to the type column in the sys.objects catalog view. For values, see [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|Yes|  
|RequestID|**int**|ID of the request containing the statement.|49|Yes|  
|ServerName|**nvarchar**|Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.|26|No|  
|SessionLoginName|**nvarchar**|Login name of the user who originated the session. For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, SessionLoginName shows Login1 and LoginName shows Login2. This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.|64|Yes|  
|SPID|**int**|ID of the session on which the event occurred.|12|Yes|  
|StartTime|**datetime**|Time at which the event started, if available.|14|Yes|  
|TextData|**ntext**|Text of the SQL being removed from the cache.|1|Yes|  
|TransactionID|**bigint**|System-assigned ID of the transaction.|4|Yes|  
|XactSequence|**bigint**|Token that describes the current transaction.|50|Yes|  
  
## See Also  
 [Extended Events](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
