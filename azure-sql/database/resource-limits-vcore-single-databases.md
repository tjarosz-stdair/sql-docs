---
title: Single database vCore resource limits
description: This page describes some common vCore resource limits for a single database in Azure SQL Database.
author: dimitri-furman
ms.author: dfurman
ms.reviewer: wiassaf, mathoma
ms.date: 07/18/2022
ms.service: sql-database
ms.subservice: service-overview
ms.topic: reference
ms.custom:
  - "sqldbrb=1"
  - "references_regions"
---
# Resource limits for single databases using the vCore purchasing model
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

This article provides the detailed resource limits for single databases in Azure SQL Database using the vCore purchasing model.

* For DTU purchasing model limits for single databases on a server, see [Overview of resource limits on a server](resource-limits-logical-server.md).
* For DTU purchasing model resource limits for Azure SQL Database, see [DTU resource limits single databases](resource-limits-dtu-single-databases.md) and [DTU resource limits elastic pools](resource-limits-dtu-elastic-pools.md).
* For elastic pool vCore resource limits, [vCore resource limits - elastic pools](resource-limits-vcore-elastic-pools.md).
* For more information regarding the different purchasing models, see [Purchasing models and service tiers](purchasing-models.md).

> [!IMPORTANT]
> Under some circumstances, you may need to shrink a database to reclaim unused space. For more information, see [Manage file space in Azure SQL Database](file-space-manage.md).

Each read-only replica of a database has its own resources, such as vCores, memory, data IOPS, tempdb, workers, and sessions. Each read-only replica is subject to the resource limits detailed later in this article.

You can set the service tier, compute size (service objective), and storage amount for a single database using:

* [Transact-SQL](single-database-manage.md#transact-sql-t-sql) via [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql#overview-sql-database)
* [Azure portal](single-database-manage.md#the-azure-portal)
* [PowerShell](single-database-manage.md#powershell)
* [Azure CLI](single-database-manage.md#azure-cli)
* [REST API](single-database-manage.md#rest-api)

> [!IMPORTANT]
> For scaling guidance and considerations, see [Scale a single database](single-database-scale.md).

## General purpose - serverless compute - Gen5

<!---
vCore resource limits are listed in the following articles, please be sure to update all of them: 
/database/resource-limits-vcore-single-databases.md
/database/resource-limits-vcore-elastic-pools.md
/database/resource-limits-logical-server.md
/database/service-tier-general-purpose.md
/database/service-tier-business-critical.md
/database/service-tier-hyperscale.md
/managed-instance/resource-limits.md
--->

The [serverless compute tier](serverless-tier-overview.md) is currently available on Gen5 hardware only.

### Gen5 hardware (part 1)

|Compute size (service objective)|GP_S_Gen5_1|GP_S_Gen5_2|GP_S_Gen5_4|GP_S_Gen5_6|GP_S_Gen5_8|
|:--- | --: |--: |--: |--: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|
|Min-max vCores|0.5-1|0.5-2|0.5-4|0.75-6|1.0-8|
|Min-max memory (GB)|2.02-3|2.05-6|2.10-12|2.25-18|3.00-24|
|Min-max auto-pause delay (minutes)|60-10080|60-10080|60-10080|60-10080|60-10080|
|Columnstore support|Yes <sup>1</sup>|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|512|1024|1024|1024|2048|
|Max log size (GB) <sup>2</sup>|154|307|307|307|461|
|Tempdb max data size (GB)|32|64|128|192|256|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>3</sup>|320|640|1280|1920|2560|
|Max log rate (MBps)|4.5|9|18|27|36|
|Max concurrent workers|75|150|300|450|600|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> Service objectives with smaller max vCore configurations may have insufficient memory for creating and using columnstore indexes.  If encountering performance problems with columnstore, increase the max vCore configuration to increase the max memory available.  

<sup>2</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>3</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen5 hardware (part 2)

|Compute size (service objective)|GP_S_Gen5_10|GP_S_Gen5_12|GP_S_Gen5_14|GP_S_Gen5_16|
|:--- | --: |--: |--: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|
|Min-max vCores|1.25-10|1.50-12|1.75-14|2.00-16|
|Min-max memory (GB)|3.75-30|4.50-36|5.25-42|6.00-48|
|Min-max auto-pause delay (minutes)|60-10080|60-10080|60-10080|60-10080|
|Columnstore support|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|
|Max data size (GB)|2048|3072|3072|3072|
|Max log size (GB) <sup>1</sup>|461|461|461|922|
|Tempdb max data size (GB)|320|384|448|512|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|3200|3840|4480|5120|
|Max log rate (MBps)|45|50|50|50|
|Max concurrent workers|750|900|1050|1200|
|Max concurrent sessions|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|
|Multi-AZ|Yes|Yes|Yes|Yes|
|Read Scale-out|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen5 hardware (part 3)

|Compute size (service objective)|GP_S_Gen5_18|GP_S_Gen5_20|GP_S_Gen5_24|GP_S_Gen5_32|GP_S_Gen5_40|
|:--- | --: |--: |--: |--: |--:|
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|
|Min-max vCores|2.25-18|2.5-20|3-24|4-32|5-40|
|Min-max memory (GB)|6.75-54|7.5-60|9-72|12-96|15-120|
|Min-max auto-pause delay (minutes)|60-10080|60-10080|60-10080|60-10080|60-10080|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|3072|3072|4096|4096|4096|
|Max log size (GB) <sup>1</sup>|922|922|1024|1024|1024|
|Tempdb max data size (GB)|576|640|768|1024|1280|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|5760|6400|7680|10240|12800|
|Max log rate (MBps)|50|50|50|50|50|
|Max concurrent workers|1350|1500|1800|2400|3000|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|


<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## Hyperscale - provisioned compute - Gen5

### Gen5 hardware (part 1)

|Compute size (service objective)|HS_Gen5_2|HS_Gen5_4|HS_Gen5_6|HS_Gen5_8|HS_Gen5_10|HS_Gen5_12|HS_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|2|4|6|8|10|12|14|
|Memory (GB)|10.4|20.8|31.1|41.5|51.9|62.3|72.7|
|[RBPEX](hyperscale-architecture.md#compute) Size|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (TB)|100 |100 |100 |100 |100 |100 |100|
|Max log size (TB)|Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |
|`Tempdb` max data size (GB)|64|128|192|256|320|384|448|
|Max local SSD IOPS <sup>1</sup>|8000 |16000 |24000 |32000 |40000 |48000 |56000 |
|Max log rate (MBps)|100 |100 |100 |100 |100 |100 |100 |
|Local read IO latency<sup>2</sup> |1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Remote read IO latency<sup>2</sup>|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|
|Write IO latency<sup>2</sup>|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|
|Storage type|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|
|Max concurrent workers|200|400|600|800|1000|1200|1400|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Secondary replicas|0-4|0-4|0-4|0-4|0-4|0-4|0-4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Backup storage retention|7 days|7 days|7 days|7 days|7 days|7 days|7 days|


<sup>1</sup> Besides local SSD IO, workloads will use remote [page server](hyperscale-architecture.md#page-server) IO. Effective IOPS will depend on workload. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance), and [Data IO in resource utilization statistics](hyperscale-performance-diagnostics.md#data-io-in-resource-utilization-statistics).

<sup>2</sup> Latency numbers are approximate and representative for typical workloads at steady state, but are not guaranteed. 

<sup>3</sup> Hyperscale is a multi-tiered architecture with separate compute and storage components. For more information, see [Hyperscale service tier architecture](hyperscale-architecture.md).



### Gen5 hardware (part 2)

|Compute size (service objective)|HS_Gen5_16|HS_Gen5_18|HS_Gen5_20|HS_Gen5_24|HS_Gen5_32|HS_Gen5_40|HS_Gen5_80|
|:--- | --: |--: |--: |--: |---: |--: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|16|18|20|24|32|40|80|
|Memory (GB)|83|93.4|103.8|124.6|166.1|207.6|415.2|
|[RBPEX](hyperscale-architecture.md#compute) Size|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (TB)|100 |100 |100 |100 |100 |100 |100 |
|Max log size (TB)|Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |
|Tempdb max data size (GB)|512|576|640|768|1024|1280|2560|
|Max local SSD IOPS <sup>1</sup>|64000 |72000 |80000 |96000 |128000 |160000 |204800 |
|Max log rate (MBps)|100 |100 |100 |100 |100 |100 |100 |
|Local read IO latency<sup>2</sup> |1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Remote read IO latency<sup>2</sup>|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|
|Write IO latency<sup>2</sup>|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|
|Storage type|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|
|Max concurrent workers|1600|1800|2000|2400|3200|4000|8000|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Secondary replicas|0-4|0-4|0-4|0-4|0-4|0-4|0-4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Backup storage retention|7 days|7 days|7 days|7 days|7 days|7 days|7 days|

<sup>1</sup> Besides local SSD IO, workloads will use remote [page server](hyperscale-architecture.md#page-server) IO. Effective IOPS will depend on workload. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance), and [Data IO in resource utilization statistics](hyperscale-performance-diagnostics.md#data-io-in-resource-utilization-statistics).

<sup>2</sup> Latency numbers are representative for typical workloads at steady state, but are not guaranteed. 

<sup>3</sup> Hyperscale is a multi-tiered architecture with separate compute and storage components. For more information, see [Hyperscale service tier architecture](hyperscale-architecture.md).

## Hyperscale - provisioned compute - DC-series

|Compute size (service objective)|HS_DC_2|HS_DC_4|HS_DC_6|HS_DC_8|
|:--- | --: |--: |--: |--: |
|Hardware|DC-series|DC-series|DC-series|DC-series|
|vCores|2|4|6|8|
|Memory (GB)|9|18|27|36|
|[RBPEX](hyperscale-architecture.md#compute) Size|3X Memory|3X Memory|3X Memory|3X Memory|
|Columnstore support|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|
|Max data size (TB)|100 |100 |100 |100 |
|Max log size (TB)|Unlimited |Unlimited |Unlimited |Unlimited |
|Tempdb max data size (GB)|64|128|192|256|
|Max local SSD IOPS <sup>1</sup>|14000|28000|42000|44800|
|Max log rate (MBps)|100 |100 |100 |100 |
|Local read IO latency<sup>2</sup> |1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Remote read IO latency<sup>2</sup>|1-5 ms|1-5 ms|1-5 ms|1-5 ms|
|Write IO latency<sup>2</sup>|3-5 ms|3-5 ms|3-5 ms|3-5 ms|
|Storage type|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|
|Max concurrent workers|160|320|480|640|
|Max concurrent sessions|30,000|30,000|30,000|30,000|
|Secondary replicas|0-4|0-4|0-4|0-4|
|Multi-AZ|N/A|N/A|N/A|N/A|
|Read Scale-out|Yes|Yes|Yes|Yes|
|Backup storage retention|7 days|7 days|7 days|7 days|

<sup>1</sup> Besides local SSD IO, workloads will use remote [page server](hyperscale-architecture.md#page-server) IO. Effective IOPS will depend on workload. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance), and [Data IO in resource utilization statistics](hyperscale-performance-diagnostics.md#data-io-in-resource-utilization-statistics).

<sup>2</sup> Latency numbers are representative for typical workloads at steady state, but are not guaranteed. 

<sup>3</sup> Hyperscale is a multi-tiered architecture with separate compute and storage components. For more information, see [Hyperscale service tier architecture](hyperscale-architecture.md).

## General purpose - provisioned compute - Gen5

### Gen5 hardware (part 1)

|Compute size (service objective)|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|2|4|6|8|10|12|14|
|Memory (GB)|10.4|20.8|31.1|41.5|51.9|62.3|72.7|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|1024|1024|1536|2048|2048|3072|3072|
|Max log size (GB) <sup>1</sup>|307|307|461|461|461|922|922|
|Tempdb max data size (GB)|64|128|192|256|320|384|384|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|640|1280|1920|2560|3200|3840|4480|
|Max log rate (MBps)|9|18|27|36|45|50|50|
|Max concurrent workers|200|400|600|800|1000|1200|1400|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|1|1|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen5 hardware (part 2)

|Compute size (service objective)|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|16|18|20|24|32|40|80|
|Memory (GB)|83|93.4|103.8|124.6|166.1|207.6|415.2|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|3072|3072|3072|4096|4096|4096|4096|
|Max log size (GB) <sup>1</sup>|922|922|922|1024|1024|1024|1024|
|Tempdb max data size (GB)|512|576|640|768|1024|1280|2560|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|5120|5760|6400|7680|10240|12800|12800|
|Max log rate (MBps)|50|50|50|50|50|50|50|
|Max concurrent workers|1600|1800|2000|2400|3200|4000|8000|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|1|1|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## General purpose - provisioned compute - Fsv2-series

### Fsv2-series Hardware (part 1)

|Compute size (service objective)|GP_Fsv2_8|GP_Fsv2_10|GP_Fsv2_12|GP_Fsv2_14| GP_Fsv2_16|
|:---| ---:|---:|---:|---:|---:|
|Hardware|Fsv2-series|Fsv2-series|Fsv2-series|Fsv2-series|Fsv2-series|
|vCores|8|10|12|14|16|
|Memory (GB)|15.1|18.9|22.7|26.5|30.2|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|1024|1024|1024|1024|1536|
|Max log size (GB) <sup>1</sup>|336|336|336|336|512|
|Tempdb max data size (GB)|37|46|56|65|74|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|2560|3200|3840|4480|5120|
|Max log rate (MBps)|36|45|50|50|50|
|Max concurrent workers|400|500|600|700|800|
|Max concurrent logins|800|1000|1200|1400|1600|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Fsv2-series hardware (part 2)

|Compute size (service objective)|GP_Fsv2_18|GP_Fsv2_20|GP_Fsv2_24|GP_Fsv2_32| GP_Fsv2_36|GP_Fsv2_72|
|:---| ---:|---:|---:|---:|---:|---:|
|Hardware|Fsv2-series|Fsv2-series|Fsv2-series|Fsv2-series|Fsv2-series|Fsv2-series|
|vCores|18|20|24|32|36|72|
|Memory (GB)|34.0|37.8|45.4|60.5|68.0|136.0|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|1536|1536|1536|3072|3072|4096|
|Max log size (GB) <sup>1</sup>|512|512|512|1024|1024|1024|
|Tempdb max data size (GB)|83|93|111|148|167|333|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|5760|6400|7680|10240|11520|12800|
|Max log rate (MBps)|50|50|50|50|50|50|
|Max concurrent workers|900|1000|1200|1600|1800|3600|
|Max concurrent logins|1800|2000|2400|3200|3600|7200|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|1|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## General purpose - provisioned compute - DC-series

|Compute size (service objective)|GP_DC_2|GP_DC_4|GP_DC_6|GP_DC_8| 
|:---| ---:|---:|---:|---:|
|Hardware|DC-series|DC-series|DC-series|DC-series|
|vCores|2|4|6|8|
|Memory (GB)|9|18|27|36|
|Columnstore support|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|
|Max data size (GB)|1024|1536|3072|3072|
|Max log size (GB) <sup>1</sup>|307|461|922|922|
|Tempdb max data size (GB)|64|128|192|256|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|640|1280|1920|2560|
|Max log rate (MBps)|9|18|27|36|
|Max concurrent workers|160|320|480|640|
|Max concurrent sessions|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|
|Multi-AZ|N/A|N/A|N/A|N/A|
|Read Scale-out|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## Business critical - provisioned compute - Gen5

### Gen5 hardware (part 1)

|Compute size (service objective)|BC_Gen5_2|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|2|4|6|8|10|12|14|
|Memory (GB)|10.4|20.8|31.1|41.5|51.9|62.3|72.7|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|1.57|3.14|4.71|6.28|8.65|11.02|13.39|
|Max data size (GB)|1024|1024|1536|2048|2048|3072|3072|
|Max log size (GB) <sup>1</sup>|307|307|461|461|461|922|922|
|Tempdb max data size (GB)|64|128|192|256|320|384|448|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|4829|4829|4829|4829|4829|4829|4829|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|8000|16,000|24,000|32,000|40,000|48,000|56,000|
|Max log rate (MBps)|24|48|72|96|96|96|96|
|Max concurrent workers|200|400|600|800|1000|1200|1400|
|Max concurrent logins|200|400|600|800|1000|1200|1400|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|4|4|4|4|4|4|4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen5 hardware (part 2)

|Compute size (service objective)|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Hardware|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|Gen5|
|vCores|16|18|20|24|32|40|80|
|Memory (GB)|83|93.4|103.8|124.6|166.1|207.6|415.2|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|15.77|18.14|20.51|25.25|37.94|52.23|131.64|
|Max data size (GB)|3072|3072|3072|4096|4096|4096|4096|
|Max log size (GB) <sup>1</sup>|922|922|922|1024|1024|1024|1024|
|Tempdb max data size (GB)|512|576|640|768|1024|1280|2560|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|4829|4829|4829|4829|4829|4829|4829|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|64,000|72,000|80,000|96,000|128,000|160,000|204,800|
|Max log rate (MBps)|96|96|96|96|96|96|96|
|Max concurrent workers|1600|1800|2000|2400|3200|4000|8000|
|Max concurrent logins|1600|1800|2000|2400|3200|4000|8000|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|4|4|4|4|4|4|4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## Business Critical - provisioned compute - M-series

For important information about M-series hardware availability, see [Azure offer types supported by M-series](service-tiers-sql-database-vcore.md#azure-offer-types-supported-by-m-series).

### M-series hardware (part 1)

|Compute size (service objective)|BC_M_8|BC_M_10|BC_M_12|BC_M_14|BC_M_16|BC_M_18|
|:---| ---:|---:|---:|---:|---:|---:|
|Hardware|M-series|M-series|M-series|M-series|M-series|M-series|
|vCores|8|10|12|14|16|18|
|Memory (GB)|235.4|294.3|353.2|412.0|470.9|529.7|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|64|80|96|112|128|150|
|Max data size (GB)|512|640|768|896|1024|1152|
|Max log size (GB) <sup>1</sup>|171|213|256|299|341|384|
|Tempdb max data size (GB)|256|320|384|448|512|576|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|13836|13836|13836|13836|13836|13836|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|12,499|15,624|18,748|21,873|24,998|28,123|
|Max log rate (MBps)|48|60|72|84|96|108|
|Max concurrent workers|800|1,000|1,200|1,400|1,600|1,800|
|Max concurrent logins|800|1,000|1,200|1,400|1,600|1,800|
|Max concurrent sessions|30000|30000|30000|30000|30000|30000|
|Number of replicas|4|4|4|4|4|4|
|Multi-AZ|No|No|No|No|No|No|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### M-series hardware (part 2)

|Compute size (service objective)|BC_M_20|BC_M_24|BC_M_32|BC_M_64|BC_M_128|
|:---| ---:|---:|---:|---:|---:|
|Hardware|M-series|M-series|M-series|M-series|M-series|
|vCores|20|24|32|64|128|
|Memory (GB)|588.6|706.3|941.8|1883.5|3767.0|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|172|216|304|704|1768|
|Max data size (GB)|1280|1536|2048|4096|4096|
|Max log size (GB) <sup>1</sup>|427|512|683|1024|1024|
|Tempdb max data size (GB)|640|768|1024|2048|4096|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|13836|13836|13836|13836|13836|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|31,248|37,497|49,996|99,993|160,000|
|Max log rate (MBps)|120|144|192|264|264|
|Max concurrent workers|2,000|2,400|3,200|6,400|12,800|
|Max concurrent logins|2,000|2,400|3,200|6,400|12,800|
|Max concurrent sessions|30000|30000|30000|30000|30000|
|Number of replicas|4|4|4|4|4|
|Multi-AZ|No|No|No|No|No|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## Business Critical - provisioned compute - DC-series

|Compute size (service objective)|BC_DC_2|BC_DC_4|BC_DC_6|BC_DC_8|
|:--- | --: |--: |--: |--: |
|Hardware|DC-series|DC-series|DC-series|DC-series|
|vCores|2|4|6|8|
|Memory (GB)|9|18|27|36|
|Columnstore support|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|1.7|3.7|5.9|8.2|
|Max data size (GB)|768|768|768|768|
|Max log size (GB) <sup>1</sup>|230|230|230|230|
|Tempdb max data size (GB)|64|128|192|256|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|1406|1406|1406|1406|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|14000|28000|42000|44800|
|Max log rate (MBps)|24|48|72|96|
|Max concurrent workers|200|400|600|800|
|Max concurrent logins|200|400|600|800|
|Max concurrent sessions|30,000|30,000|30,000|30,000|
|Number of replicas|4|4|4|4|
|Multi-AZ|No|No|No|No|
|Read Scale-out|No|No|No|No|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).


## Previously available hardware

This section includes details on previously available hardware.

[!INCLUDE[azure-sql-gen4-hardware-retirement](../includes/azure-sql-gen4-hardware-retirement.md)]

## Hyperscale - provisioned compute - Gen4

### Gen4 hardware (part 1)

|Compute size (service objective)|HS_Gen4_1|HS_Gen4_2|HS_Gen4_3|HS_Gen4_4|HS_Gen4_5|HS_Gen4_6|
|:--- | --: |--: |--: |---: | --: |--: |
|hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|1|2|3|4|5|6|
|Memory (GB)|7|14|21|28|35|42|
|[RBPEX](hyperscale-architecture.md#compute) Size|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (TB)|100 |100 |100 |100 |100 |100|
|Max log size (TB)|Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |
|Tempdb max data size (GB)|32|64|96|128|160|192|
|Max local SSD IOPS <sup>1</sup>|4000 |8000 |12000 |16000 |20000 |24000 |
|Max log rate (MBps)|100 |100 |100 |100 |100 |100 |
|Local read IO latency<sup>2</sup> |1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Remote read IO latency<sup>2</sup>|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|
|Write IO latency<sup>2</sup>|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|
|Storage type|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|
|Max concurrent workers|200|400|600|800|1000|1200|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Secondary replicas|0-4|0-4|0-4|0-4|0-4|0-4|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|
|Backup storage retention|7 days|7 days|7 days|7 days|7 days|7 days|

<sup>1</sup> Besides local SSD IO, workloads will use remote [page server](hyperscale-architecture.md#page-server) IO. Effective IOPS will depend on workload. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance), and [Data IO in resource utilization statistics](hyperscale-performance-diagnostics.md#data-io-in-resource-utilization-statistics).

<sup>2</sup> Latency numbers are approximate and representative for typical workloads at steady state, but are not guaranteed. 

<sup>3</sup> Hyperscale is a multi-tiered architecture with separate compute and storage components. For more information, see [Hyperscale service tier architecture](hyperscale-architecture.md).


### Gen4 hardware (part 2)

|Compute size (service objective)|HS_Gen4_7|HS_Gen4_8|HS_Gen4_9|HS_Gen4_10|HS_Gen4_16|HS_Gen4_24|
|:--- | ---: |--: |--: | --: |--: |--: |
|Hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|7|8|9|10|16|24|
|Memory (GB)|49|56|63|70|112|159.5|
|[RBPEX](hyperscale-architecture.md#compute) Size|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|3X Memory|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (TB)|100 |100 |100 |100 |100 |100 |
|Max log size (TB)|Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |Unlimited |
|Tempdb max data size (GB)|224|256|288|320|512|768|
|Max local SSD IOPS <sup>1</sup>|28000 |32000 |36000 |40000 |64000 |76800 |
|Max log rate (MBps)|100 |100 |100 |100 |100 |100 |
|Local read IO latency<sup>2</sup> |1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Remote read IO latency<sup>2</sup>|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|1-5 ms|
|Write IO latency<sup>2</sup>|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|3-5 ms|
|Storage type|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|Multi-tiered<sup>3</sup>|
|Max concurrent workers|1400|1600|1800|2000|3200|4800|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Secondary replicas|0-4|0-4|0-4|0-4|0-4|0-4|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|
|Backup storage retention|7 days|7 days|7 days|7 days|7 days|7 days|


<sup>1</sup> Besides local SSD IO, workloads will use remote [page server](hyperscale-architecture.md#page-server) IO. Effective IOPS will depend on workload. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance), and [Data IO in resource utilization statistics](hyperscale-performance-diagnostics.md#data-io-in-resource-utilization-statistics).

<sup>2</sup> Latency numbers are approximate and representative for typical workloads at steady state, but are not guaranteed. 

<sup>3</sup> Hyperscale is a multi-tiered architecture with separate compute and storage components. For more information, see [Hyperscale service tier architecture](hyperscale-architecture.md).


## General purpose - provisioned compute - Gen4

> [!IMPORTANT]
> New Gen4 databases are no longer supported in the Australia East or Brazil South regions.

### Gen4 hardware (part 1)

|Compute size (service objective)|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6
|:--- | --: |--: |--: |--: |--: |--: |
|Hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|1|2|3|4|5|6|
|Memory (GB)|7|14|21|28|35|42|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|1024|1024|1536|1536|1536|3072|
|Max log size (GB) <sup>1</sup>|307|307|461|461|461|922|
|Tempdb max data size (GB)|32|64|96|128|160|192|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|320|640|960|1280|1600|1920|
|Max log rate (MBps)|4.5|9|13.5|18|22.5|27|
|Max concurrent workers|200|400|600|800|1000|1200|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|1|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen4 hardware (part 2)

|Compute size (service objective)|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24
|:--- | --: |--: |--: |--: |--: |--: |
|Hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|7|8|9|10|16|24|
|Memory (GB)|49|56|63|70|112|159.5|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|N/A|N/A|N/A|N/A|N/A|N/A|
|Max data size (GB)|3072|3072|3072|3072|4096|4096|
|Max log size (GB) <sup>1</sup>|922|922|922|922|1229|1229|
|Tempdb max data size (GB)|224|256|288|320|512|768|
|Storage type|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|Remote SSD|
|Read IO latency (approximate)|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|5-10 ms|
|Write IO latency (approximate)|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|5-7 ms|
|Max data IOPS <sup>2</sup>|2240|2560|2880|3200|5120|7680|
|Max log rate (MBps)|31.5|36|40.5|45|50|50|
|Max concurrent workers|1400|1600|1800|2000|3200|4800|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|1|1|1|1|1|1|
|Multi-AZ|N/A|N/A|N/A|N/A|N/A|N/A|
|Read Scale-out|N/A|N/A|N/A|N/A|N/A|N/A|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

## Business critical - provisioned compute - Gen4

> [!IMPORTANT]
> New Gen4 databases are no longer supported in the Australia East or Brazil South regions.

### Gen4 hardware (part 1)

|Compute size (service objective)|BC_Gen4_1|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--- | --: |--: |--: |--: |--: |--: |
|Hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|1|2|3|4|5|6|
|Memory (GB)|7|14|21|28|35|42|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|1|2|3|4|5|6|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Max data size (GB)|1024|1024|1024|1024|1024|1024|
|Max log size (GB) <sup>1</sup>|307|307|307|307|307|307|
|Tempdb max data size (GB)|32|64|96|128|160|192|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|1356|1356|1356|1356|1356|1356|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|4,000|8,000|12,000|16,000|20,000|24,000|
|Max log rate (MBps)|8|16|24|32|40|48|
|Max concurrent workers|200|400|600|800|1000|1200|
|Max concurrent logins|200|400|600|800|1000|1200|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|4|4|4|4|4|4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).

### Gen4 hardware (part 2)

|Compute size (service objective)|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--- | --: |--: |--: |--: |--: |--: |
|Hardware|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|7|8|9|10|16|24|
|Memory (GB)|49|56|63|70|112|159.5|
|Columnstore support|Yes|Yes|Yes|Yes|Yes|Yes|
|In-memory OLTP storage (GB)|7|8|9.5|11|20|36|
|Storage type|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|Local SSD|
|Max data size (GB)|1024|1024|1024|1024|1024|1024|
|Max log size (GB) <sup>1</sup>|307|307|307|307|307|307|
|Tempdb max data size (GB)|224|256|288|320|512|768|
|[Max local storage size](resource-limits-logical-server.md#storage-space-governance) (GB)|1356|1356|1356|1356|1356|1356|
|Read IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Write IO latency (approximate)|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|1-2 ms|
|Max data IOPS <sup>2</sup>|28,000|32,000|36,000|40,000|64,000|76,800|
|Max log rate (MBps)|56|64|64|64|64|64|
|Max concurrent workers|1400|1600|1800|2000|3200|4800|
|Max concurrent logins|1400|1600|1800|2000|3200|4800|
|Max concurrent sessions|30,000|30,000|30,000|30,000|30,000|30,000|
|Number of replicas|4|4|4|4|4|4|
|Multi-AZ|Yes|Yes|Yes|Yes|Yes|Yes|
|Read Scale-out|Yes|Yes|Yes|Yes|Yes|Yes|
|Included backup storage|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|1X DB size|

<sup>1</sup> For documented max data size values. Reducing max data size reduces max log size proportionally.

<sup>2</sup> The maximum value for IO sizes ranging between 8 KB and 64 KB. Actual IOPS are workload-dependent. For details, see [Data IO Governance](resource-limits-logical-server.md#resource-governance).


## Next steps

- For DTU resource limits for a single database, see [resource limits for single databases using the DTU purchasing model](resource-limits-dtu-single-databases.md)
- For vCore resource limits for elastic pools, see [resource limits for elastic pools using the vCore purchasing model](resource-limits-vcore-elastic-pools.md)
- For DTU resource limits for elastic pools, see [resource limits for elastic pools using the DTU purchasing model](resource-limits-dtu-elastic-pools.md)
- For resource limits for SQL Managed Instance, see [SQL Managed Instance resource limits](../managed-instance/resource-limits.md).
- For information about general Azure limits, see [Azure subscription and service limits, quotas, and constraints](/azure/azure-resource-manager/management/azure-subscription-service-limits).
- For information about resource limits on a server, see [overview of resource limits on a server](resource-limits-logical-server.md) for information about limits at the server and subscription levels.
