---
title: "What's new in SQL Server 2022 | Microsoft Docs"
description: Learn about new features for SQL Server 2022 (16.x), which gives you choices of development languages, data types, environments, and operating systems.
ms.prod: sql
ms.technology: release-landing
ms.topic: "article"
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: wiassaf
ms.custom:
- intro-whats-new
- event-tier1-build-2022
ms.date: 08/23/2022
monikerRange: ">=sql-server-ver15"
---

# What's new in [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)]

[!INCLUDE [sqlserver2022](../includes/applies-to-version/sqlserver2022.md)]

[!INCLUDE[sql-server-2022](../includes/sssql22-md.md)] builds on previous releases to grow SQL Server as a platform that gives you choices of development languages, data types, on-premises or cloud environments, and operating systems.

The following video introduces SQL Server 2022 Preview.

> [!VIDEO https://channel9.msdn.com/Shows/data-exposed/introduction-to-sql-server-2022-ep1/player?WT.mc_id=dataexposed-c9-niner]

For additional video content, see [What's new in SQL Server](https://microsoftmechanics.libsyn.com/podcast/whats-new-in-sql-server-2022).

This article summarizes the new features and enhancements for [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)].

## Get SQL Server 2022 Preview

[Get SQL Server 2022 Preview Evaluation Edition](https://go.microsoft.com/fwlink/?linkid=2162126).

For more information and known issues, see [[!INCLUDE[sql-server-2022](../includes/sssql22-md.md)] release notes](sql-server-2022-release-notes.md).

For the best experience with [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)], use the [latest tools](../tools/overview-sql-tools.md).

This release:

- Is available as Evaluation Edition. It's available for a 180 day trial period, and includes all of the capabilities of Enterprise Edition.
- On Azure Virtual Machines, it's available as Developer Edition. It's available for a 180 day trial period via a SQL Server on Azure Virtual Machines [marketplace image](https://ms.portal.azure.com/#create/Microsoft.AzureSQL).
- For SQL Server 2022 Preview on Linux, see the [Release notes for [!INCLUDE[sssql22](../includes/sssql22-md.md)] on Linux](../linux/sql-server-linux-release-notes-2022.md).
- Doesn't include support from Microsoft, except for select Early Adoption Program customers.

After you check out [!INCLUDE [sssql22-md](../includes/sssql22-md.md)], [submit feedback about the product](https://feedback.azure.com/d365community/forum/04fe6ee0-3b25-ec11-b6e6-000d3a4f0da0).

## Release candidate

This is release candidate (RC) 0.

SQL Server 2022 RC 0 (16.0.900.6) includes updates to the following features:

- [Intelligent query processing](#query-store-and-intelligent-query-processing)
  - Degree of parallelism (DOP) feedback - improved comparison algorithm.
- [Management](#management)
  - Improved snapshot backup support
- [Platform](#platform)
  - Integrated acceleration & offloading
- [Language](#language)
  - APPROX_PERCENTILE_DISC()
  - APPROX_PERCENTILE_CONT()
  - TRIM scalar function extensions

For details, see the feature descriptions in the sections below.

The following sections provide an overview of these features.

## Analytics

| New feature or update | Details |
|:---|:---|
|Azure Synapse Link for SQL|Get near real time analytics over operational data in [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)]. With a seamless integration between operational stores in [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)] and Azure Synapse Analytics dedicated SQL pools, Azure Synapse Link for SQL enables you to run analytics, business intelligence and machine learning scenarios on your operational data with minimum impact on source databases with a new change feed technology. <br/><br/> For more information, see [What is Azure Synapse Link for SQL? (Preview) - Azure Synapse Analytics](/azure/synapse-analytics/synapse-link/sql-synapse-link-overview). <br/></br> See also, [Known issues](/azure/synapse-analytics/synapse-link/synapse-link-for-sql-known-issues).|
|Object storage integration | SQL Server 2022 Preview introduces new object storage integration to the data platform, enabling you to integrate SQL Server with S3-compatible object storage, in addition to Azure Storage. The first is [backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url-s3-compatible-object-storage.md) and the second is Data Lake Virtualization. <br/><br/> Data Lake Virtualization integrates [PolyBase with S3-compatible object storage](../relational-databases/polybase/polybase-configure-s3-compatible.md), adds support for to querying parquet files with T-SQL.|
|Data Virtualization | Query different types of data on different types of data sources from SQL Server. |

## Availability

| New feature or update | Details |
|:---|:---|
| Link to Azure SQL Managed Instance | Connect your SQL Server instance to Azure SQL Managed Instance. See [Link feature for Azure SQL Managed Instance (preview)](/azure/azure-sql/managed-instance/managed-instance-link-feature-overview). To experience this feature, you can [register here](https://aka.ms/mi-link-2022-signup).|
|Contained availability group | Create an Always On availability group that:<br/>- Manages its own metadata objects (users, logins, permissions, SQL Agent jobs etc.) at the availability group level in addition to the instance level. <br/>- Includes specialized contained system databases within the availability group. For more information, see [What is a contained availability group?](../database-engine/availability-groups/windows/contained-availability-groups-overview.md)|
|Distributed availability group |- Changing `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` is supported. For more information, visit [ALTER AVAILABILITY GROUP ()](../t-sql/statements/alter-availability-group-transact-sql.md)<br/> - Now using multiple TCP connections for better network bandwidth utilization across a remote link with long tcp latencies.|
| Improved availability groups | - `ParallelRedoThreadPool` : Instance level thread pool shared with all databases having redo work. With this, each database can take the benefit of parallel redo. Limited to max 100 threads limit earlier. <br/> - Parallel Redo Batch Redo - Redo of log records are batched under one latch improving speed. This helps both, catchup redo and crash recovery redo. |
| Improved backup metadata | `backupset` system table returns last valid restore time. See [backupset (Transact-SQL)](../relational-databases/system-tables/backupset-transact-sql.md).|

## Security

| New feature or update | Details |
|:---|:---|
| Microsoft Defender for Cloud integration | Protect your SQL servers using the Defender for SQL plan. Defender for SQL plan requires that SQL Server Extension for Azure is enabled and includes functionalities for discovering and mitigating potential database vulnerabilities and detecting anomalous activities that could indicate a threat to your databases. [Learn more](/azure/defender-for-cloud/defender-for-sql-introduction) on how Defender for SQL can protect your entire database estate anywhere: on-premises, hybrid, and multicloud environments.
| Microsoft Purview integration | Apply Microsoft Purview access policies to any SQL Server instance that is enrolled in both Azure Arc and the Microsoft Purview Data Use Management.<br/><br/>- Newly introduced *SQL Performance Monitor*, and *SQL Security Auditor* roles align with the principle of least privilege using Microsoft Purview access policies.</br></br>Check out [Provision access by data owner for SQL Server on Azure Arc-enabled servers (preview)](/azure/purview/how-to-policies-data-owner-arc-sql-server) for details. |
| Ledger | The ledger feature provides tamper-evidence capabilities in your database. You can cryptographically attest to other parties, such as auditors or other business parties, that your data hasn't been tampered with. See [Ledger](../relational-databases/security/ledger/ledger-overview.md). |
| Azure Active Directory authentication | Use [Azure Active Directory (Azure AD) authentication](../relational-databases/security/authentication-access/azure-ad-authentication-sql-server-overview.md) to connect to SQL Server. |
| Always encrypted with secure enclaves | Enable in-place encryption and richer confidential queries. Support for confidential queries with JOIN, GROUP BY, and ORDER BY. Improved performance. See [Always Encrypted with secure enclaves](../relational-databases/security/encryption/always-encrypted-enclaves.md).|
| New permissions & roles | Enable least privileged access for administrative tasks with new [built-in server-level roles](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles-introduced-in-sql-server-2022). |
|Dynamic data masking | Granular UNMASK permissions for [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md#granular). |
|Support for PFX certificates, symmetric key enhancements, and other crypto improvements | New support for [certificate](../t-sql/statements/create-certificate-transact-sql.md) and key [backup](../t-sql/statements/backup-master-key-transact-sql.md) and [restore](../t-sql/statements/restore-master-key-transact-sql.md) integration scenarios with Azure Blob Storage service. This enables adherence to security best practices and compliance standards guidelines that prohibit the usage of insecure or deprecated algorithms like RC4. Additional improvements to enhance default cryptography in SQL Server to meet the evolving threat landscape, including but not limited to, system-generated certificates now have a default strength of RSA-3072.<br/><br/>Added [BACKUP SYMMETRIC KEY](../t-sql/statements/backup-symmetric-key-transact-sql.md) and [RESTORE SYMMETRIC KEY](../t-sql/statements/restore-symmetric-key-transact-sql.md). |
| Support MS-TDS 8.0 protocol | New MS-TDS protocol iteration. See [TDS 8.0 and TLS 1.3 support](../relational-databases/security/networking/tds-8-and-tls-1-3.md):<br/>- Makes encryption mandatory<br/>- Aligns MS-TDS with HTTPS making it manageable by network appliances for additional security<br/>- Removes MS-TDS / TLS custom interleaving and enables usage of TLS 1.3 and subsequent TLS protocol versions. |

## Performance

| New feature or update | Details |
|:---|:---|
| System page latch concurrency enhancements | Concurrent updates to global allocation map (GAM) pages and shared global allocation map (SGAM) pages reduce page latch contention while allocating/deallocating data pages and extents. These enhancements apply to all user databases and especially benefit tempdb heavy workloads.|
| Buffer pool parallel scan | Improves the performance of buffer pool scan operations on large-memory machines by utilizing multiple CPU cores. Learn more about [Operations that trigger a buffer pool scan may run slowly on large-memory computers](https://go.microsoft.com/fwlink/?linkid=2132602). |
| Ordered clustered columnstore index | Ordered clustered columnstore index (CCI) sorts the existing data in memory before the index builder compresses the data into index segments. This has the potential of more efficient segment elimination, resulting in better performance as the number of segments to read from disk is reduced. For more information, see [CREATE COLUMNSTORE INDEX (Transact-SQL)](../t-sql/statements/create-columnstore-index-transact-sql.md) and [What's new in columnstore indexes](../relational-databases/indexes/columnstore-indexes-what-s-new.md).</br></br> Also available in Synapse Analytics. See [Query performance](/azure/synapse-analytics/sql-data-warehouse/performance-tuning-ordered-cci#query-performance).|
|Improved columnstore segment elimination | All columnstore indexes benefit from enhanced segment elimination by data type. Data type choices may have a significant impact on query performance based common filter predicates for queries on the columnstore index. This segment elimination applied to numeric, date, and time data types, and the datetimeoffset data type with scale less than or equal to two. Beginning in [!INCLUDE[sssql22-md](../includes/sssql22-md.md)], segment elimination capabilities extend to string, binary, guid data types, and the datetimeoffset data type for scale greater than two. |
| In-memory OLTP management | Improve memory management in large memory servers to reduce out-of-memory conditions. |
| Virtual log file growth | In previous versions of SQL Server, if the next growth is more than 1/8 of the current log size, and the growth is less than 64MB, four VLFs were created. In SQL Server 2022, this behavior is slightly different. Only one VLF is created if the growth is less than or equal to 64 MB and more than 1/8 of the current log size. For more information on VLF growth, see [Virtual Log Files (VLFs)](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#virtual-log-files-vlfs).|

## Query Store and intelligent query processing

The [intelligent query processing (IQP)](../relational-databases/performance/intelligent-query-processing.md) feature family includes features with broad impact that improve the performance of existing workloads with minimal implementation effort.

:::image type="content" source="../relational-databases/performance/media/iqp-feature-family.svg" alt-text="A diagram of the Intelligent Query Processing family of features and when they were first introduced to SQL Server.":::

| New feature or update | Details |
|:---|:---|
| Query Store on secondary replicas |  Query Store on secondary replicas enables the same Query Store functionality on secondary replica workloads that is available for primary replicas. Learn more in [Query Store for secondary replicas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#query-store-for-secondary-replicas).<br/><br/> For more information, see [Query Store improvements](#query-store-improvements) later in this article.|
| Query Store hints | [Query Store hints](../relational-databases/performance/query-store-hints.md) leverage the Query Store to provide a method to shape query plans without changing application code. Previously only available on Azure SQL Database and Azure SQL Managed Instance, Query Store hints are now available in SQL Server 2022 Preview. Requires the Query Store to be enabled and in "Read write" mode. |
| Memory grant feedback | Memory grant feedback adjusts the size of the memory allocated for a query based on past performance. SQL Server 2022 preview introduces [Percentile and Persistence mode memory grant feedback](../relational-databases/performance/intelligent-query-processing-feedback.md#percentile-and-persistence-mode-memory-grant-feedback). Requires enabling Query Store.<br/><br/> - **Persistence**: A capability that allows the memory grant feedback for a given cached plan to be persisted in the Query Store so that feedback can be reused after cache evictions. Persistance benefits memory grant feedback as well as the new DOP and CE feedback features.<br/>- **Percentile**: A new algorithm improves performance of queries with widely oscillating memory requirements, using memory grant information from several previous query executions over, instead of just the memory grant from the immediately preceding query execution. Requires enabling Query Store. Query Store is enabled by default for newly created databases as of SQL Server 2022 CTP 2.1.|
| Parameter sensitive plan optimization | Automatically enables multiple, active cached plans for a single parameterized statement. Cached execution plans accommodate largely different data sizes based on the customer-provided runtime parameter value(s). For more information, see [Parameter Sensitive Plan optimization](../relational-databases/performance/parameter-sensitivity-plan-optimization.md).|
| Degree of parallelism (DOP) feedback | A new database scoped configuration option `DOP_FEEDBACK` automatically adjusts degree of parallelism for repeating queries to optimize for workloads where inefficient parallelism can cause performance issues. Similar to optimizations in Azure SQL Database. Requires the Query Store to be enabled and in "Read write" mode. <br/><br/> Beginning with RC 0, every query recompilation SQL Server compares the runtime stats of the query using existing feedback to the runtime stats of the previous compilation with the existing feedback. If the performance is not the same or better, we clear all DOP feedback and trigger a reanalysis of the query starting from the compiled DOP. <br/><br/> See `DOP_FEEDBACK` in [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
| Cardinality estimation feedback | Identifies and corrects suboptimal query execution plans for repeating queries, when these issues are caused by incorrect estimation model assumptions. Requires the Query Store to be enabled and in "Read write" mode. See [Cardinality Estimation (SQL Server)](../relational-databases/performance/cardinality-estimation-sql-server.md). |
| Optimized plan forcing| Uses compilation replay to improve the compilation time for forced plan generation by pre-caching non-repeatable plan compilation steps. Learn more in [Optimized plan forcing with Query Store](../relational-databases/performance/optimized-plan-forcing-query-store.md).|

## Management

| New feature or update | Details |
|:---|:---|
| Integrated setup experience for the Azure extension for SQL Server | Install the Azure extension for SQL Server at setup. Required for Azure integration features. For more information, see:</br>- [Install SQL Server from the Command Prompt](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#install-sql-server-from-the-command-prompt) <br/>- [Install SQL Server from the Installation Wizard (Setup)](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md?view=sql-server-ver16&preserve-view=true).|
| Manage Azure extension for SQL Server | Use SQL Server Configuration Manager to manage Azure extension for SQL Server service. Required to create Azure Arc-enabled SQL Server instance, and for other Azure connected features.  See [SQL Server Configuration Manager](../relational-databases/sql-server-configuration-manager.md). |
| Max server memory calculations | During setup, SQL Setup recommends a value for max server memory to align with documented recommendations. The underlying calculation is different in SQL Server 2022 to reflect recommended [server memory configuration options](../database-engine/configure-windows/server-memory-server-configuration-options.md). |
| Accelerated Database Recovery (ADR) improvements | There are several improvements to address persistent version store (PVS) storage and improve overall scalability. SQL Server 2022 implements a persistent version store cleaner thread per database instead of per instance and the memory footprint for PVS page tracker has been improved. There are also a number of ADR efficiency improvements, such as concurrency improvements that help the cleanup process to work more efficiently. ADR cleans pages that couldn't previously be cleaned due to locking.<br/><br/>See [ADR improvements in SQL Server 2022 (16.x) Preview](../relational-databases/accelerated-database-recovery-concepts.md#adr-improvements-in-).|
| Improved snapshot backup support |  Adds Transact-SQL support for freezing and thawing I/O without requiring a VDI client. [Create a Transact-SQL snapshot backup](../relational-databases/backup-restore/create-a-transact-sql-snapshot-backup.md).|
| Shrink database WAIT_AT_LOW_PRIORITY | In previous releases, shrinking databases and database files to reclaim space often leads to concurrency issues. SQL Server 2022 Preview adds WAIT_AT_LOW_PRIORITY as an additional option for shrink operations (DBCC SHRINKDATABASE and DBCC SHRINKFILE). When you specify WAIT_AT_LOW_PRIORITY, new queries requiring Sch-S or Sch-M locks aren't blocked by the waiting shrink operation, until the shrink operation stops waiting and begins executing. See [Shrink a database](../relational-databases/databases/shrink-a-database.md) and [Shrink a file](../relational-databases/databases/shrink-a-file.md).|
| XML compression |XML compression provides a method to compress off-row XML data for both XML columns and indexes, improving capacity requirements. For more information, see [CREATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/create-table-transact-sql.md) and [CREATE INDEX &#40;Transact-SQL&#41;](../t-sql/statements/create-index-transact-sql.md).|
| Asynchronous auto update statistics concurrency|Avoid potential concurrency issues using asynchronous statistics update if you enable the ASYNC_STATS_UPDATE_WAIT_AT_LOW_PRIORITY [database-scoped configuration](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
| Backup and restore to S3-compatible object storage | SQL Server 2022 extends the `BACKUP`/`RESTORE` `TO`/`FROM` `URL` syntax by adding support for a new S3 connector using the REST API. See [backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url-s3-compatible-object-storage.md).|

## Platform

| New feature or update | Details |
|:---|:---|
|Integrated acceleration & offloading | [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)] leverages acceleration technologies from partners such as Intel to provide extended capabilities. At release, Intel&reg; QuickAssist Technology (QAT) provides backup compression and hardware offloading. For more information, see [Integrated acceleration & offloading](../relational-databases/integrated-acceleration/overview.md). |
| Improved optimization | [!INCLUDE[sql-server-2022](../includes/sssql22-md.md)] leverages new hardware capabilities - including the Advanced Vector Extension (AVX) 512 extension to improve batch mode operations. |

## Language

| New feature or update | Details |
|:---|:---|
| Resumable add table constraints | Supports [pausing and resuming an ALTER TABLE ADD CONSTRAINT](../relational-databases/security/resumable-add-table-constraints.md) operation. Resume such operation after maintenance windows, failovers, or system failures.
| Transactional replication | Peer-to-peer replication enables conflict detection and resolution to allow last writer to win. Originally introduced in [!INCLUDE [sssql19-md](../includes/sssql19-md.md)] CU 13. See [Automatically handle conflicts with last write wins](../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md#automatically-handle-conflicts-with-last-write-wins) for more information. |
| CREATE STATISTICS | Adds [AUTO_DROP option](../relational-databases/statistics/statistics.md#auto_drop-option)<br/><br/>Automatic statistics with low priority.|
| SELECT ... WINDOW clause | Determines the partitioning and ordering of a rowset before the window function, which uses the window in OVER clause is applied. See [SELECT - WINDOW ](../t-sql/queries/select-window-transact-sql.md).|
| IS \[NOT\] DISTINCT FROM | Determines whether two expressions when compared with each other evaluate to NULL, and guarantees a true or false value as the result. For more information, see [IS [NOT] DISTINCT FROM (Transact-SQL)](../t-sql/queries/is-distinct-from-transact-sql.md). |
| Time series functions | You can store and analyze data that changes over time, using time-windowing, aggregation, and filtering capabilities.<br/>- [DATE_BUCKET ()](../t-sql/functions/date-bucket-transact-sql.md)<br/>- [GENERATE_SERIES ()](../t-sql/functions/generate-series-transact-sql.md)<br/><br/>The following adds support to IGNORE NULLS and RESPECT NULLS:<br/>- [FIRST_VALUE ()](../t-sql/functions/first-value-transact-sql.md)<br/>- [LAST_VALUE ()](../t-sql/functions/last-value-transact-sql.md)|
| JSON functions | - [ISJSON ()](../t-sql/functions/isjson-transact-sql.md)<br/>- [JSON_PATH_EXISTS ()](../t-sql/functions/json-path-exists-transact-sql.md)<br/>- [JSON_OBJECT ()](../t-sql/functions/json-object-transact-sql.md)<br/>- [JSON_ARRAY ()](../t-sql/functions/json-array-transact-sql.md)|
| Aggregate functions | - [APPROX_PERCENTILE_CONT ()](../t-sql/functions/approx-percentile-cont-transact-sql.md)<br/>- [APPROX_PERCENTILE_DISC ()](../t-sql/functions/approx-percentile-disc-transact-sql.md)
| T-SQL functions |- [GREATEST ()](../t-sql/functions/logical-functions-greatest-transact-sql.md)<br/>- [LEAST ()](../t-sql/functions/logical-functions-least-transact-sql.md)<br/>- [STRING_SPLIT ()](../t-sql/functions/string-split-transact-sql.md)<br/>- [DATETRUNC ()](../t-sql/functions/datetrunc-transact-sql.md)<br/>- [LTRIM ()](../t-sql/functions/ltrim-transact-sql.md)<br/>- [RTRIM ()](../t-sql/functions/rtrim-transact-sql.md)<br/>- [TRIM ()](../t-sql/functions/trim-transact-sql.md)|
| [Bit manipulation functions](../t-sql/functions/bit-manipulation-functions-overview.md) |- [LEFT_SHIFT ()](../t-sql/functions/left-shift-transact-sql.md)<br/>- [RIGHT_SHIFT ()](../t-sql/functions/right-shift-transact-sql.md)<br/>- [BIT_COUNT ()](../t-sql/functions/bit-count-transact-sql.md)<br/>- [GET_BIT ()](../t-sql/functions/get-bit-transact-sql.md)<br/>- [SET_BIT ()](../t-sql/functions/set-bit-transact-sql.md)|

## Tools

| New feature or update | Details |
|:---|:---|
| Azure Data Studio | Get the latest release at [Download and install Azure Data Studio](../azure-data-studio/download-azure-data-studio.md). The latest release includes support for SQL Server 2022.  |
| Distributed Replay |  SQL Server setup no longer includes the Distributed Replay client and controller executables. These will be available, along with the Admin executable, as a separate download |
| SQL Server Management Studio | SSMS version 19.0 is now available and is the recommended version of SSMS for SQL Server 2022. [Download SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms-19.md). |
| SqlPackage.exe | Version 19 of SqlPackage provides support for SQL Server 2022. Get the latest version at [Download and install sqlpackage](../tools/sqlpackage/sqlpackage-download.md).|
| VS Code | The latest release of VS Code, version 1.67, supports SQL Server 2022. Get it at <https://code.visualstudio.com/>. |

## SQL Machine Learning Services

Beginning with SQL Server 2022, runtimes for R, Python, and Java, are no longer installed with SQL Setup. Instead, install any desired custom runtime(s) and packages. For more information, see [Install SQL Server Machine Learning Services (Python and R) on Windows](../machine-learning/install/sql-machine-learning-services-windows-install-sql-2022.md) or [Install SQL Server Machine Learning Services (Python and R) on Linux](../linux/sql-server-linux-setup-machine-learning-sql-2022.md).

## Additional information

This section provides additional information for the features highlighted above.

### Query Store improvements

Query Store helps you better track performance history, troubleshoot query plan related issues, and enable new capabilities in [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)], [!INCLUDE[ssazuremi_md](../includes/ssazuremi_md.md)], and [!INCLUDE[sssql22-md](../includes/sssql22-md.md)]. CTP 2.1 introduces Query Store enabled by default for new databases. If you need to enable the query store, see [Enable the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Enabling).

- For databases that have been restored from other SQL Server instances and for those databases that are upgraded from an in-place upgrade to SQL Server 2022, these databases will retain the previous Query Store settings.

- For databases that are restored from previous SQL Server instances, separately evaluate the [database compatibility level settings](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) as some Intelligent Query Processing features are enabled by the compatibility level setting.

If there's concern about the overhead Query Store may introduce, administrators can leverage custom capture policies to further tune what the Query Store captures. Custom capture policies are available to help further tune Query Store captures. Custom capture policies can be used to be more selective about which queries, and query details are captured. For example, an administrator may choose to capture only the most expensive queries, repeated queries, or the queries that have a high level of compute overhead. [Custom capture policies](../t-sql/statements/alter-database-transact-sql-set-options.md#query_capture_policy_option_list--) can help Query Store capture the most important queries in your workload. Note that except for the STALE_CAPTURE_POLICY_THRESHOLD option, these options define the OR conditions that need to happen for queries to be captured in the defined Stale Capture Policy Threshold value. For example, these are the default values in the `QUERY_CAPTURE_MODE = AUTO`:

```sql
...
QUERY_CAPTURE_MODE = CUSTOM,
QUERY_CAPTURE_POLICY = ( 
STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS, 
EXECUTION_COUNT = 30, 
TOTAL_COMPILE_CPU_TIME_MS = 1000, 
TOTAL_EXECUTION_CPU_TIME_MS = 100 
)
...
```

## SQL Server Analysis Services

This release introduces new features and improvements for performance, resource governance, and client support. For specific updates, see [What's new in SQL Server Analysis Services](/analysis-services/what-s-new-in-sql-server-analysis-services).

## SQL Server Reporting Services

This release introduces new features and improvements for accessibility, security, reliability, and bug fixes. For specific updates, see [What's new in SQL Server Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## See also

- [`SqlServer` PowerShell module](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell documentation](../powershell/sql-server-powershell.md)
- [SQL Server Workshops](https://aka.ms/sqlworkshops)
- [[!INCLUDE[SQL Server 2022](../includes/sssql22-md.md)] release notes](sql-server-2022-release-notes.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
