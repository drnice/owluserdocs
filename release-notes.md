# Release Notes

## 2021.09 \(09-2021\) In progress...

#### New Feature

* Alert
  * Alert notification page displaying a searchable list of alerts emails sent.  [Email Alerts](alerts/email-alerts.md#example-alert-in-your-inbox)
* Job Page
  * UI refresh
  * New chart with successful and failed jobs

#### Enhancements

* Profile
  * When faced with a few errors e.g. 0.005% null, highlight issues more clearly and visibly instead  of the notion of rounding up to 100%
* Connections
  * New templates for Redshift and Solr
* Catalog
  * Completeness report refactor / consolidation to improve performance
* Security
  * Added property for authentication age to reduce token expiration
  * UI labels more generic when configuring a connection with password manager script
* Agent
  * Agent no longer shows as red if services are correctly running
* Logging
  * Jobs log retention policy now configurable in Admin Console -&gt; App Config via "JOB\_LOG\_RETENTION\_HR" \(variable must be added along with value\). If not added, default to 72 hours
  * Platform logs retention policy now configurable in Admin Console -&gt; App Config via "PLATFORM\_LOG\_RETENTION\_HR" \(variable must be added along with value\). If not added, default to 24 hours
* Jobs
  * Job Template corrupt time portion of ${rd} on last run of replay
  * Refactor job actions column
* Scorecards
  * Fixed missing search results issue in list view for Patterns type
* Export
  * Outlier tab in DQ Job page \(hoot page\) displays linkIds and included in the export

## 2021.08 \(**08-2021\)**

_Please note updated Collibra release name methodology_

#### Enhancements

* Explorer
  * Support for handling large tables
  * Implemented pagination function for navigation
  * Improved error handling for unsupported java data types
  * Fix preview for uploaded temp files
* Collibra DQ V3 REST APIs
  * Additional rest APIs for easier programmatic job initiation, job response status, and job result decisioning \(used in pipelines\). Streamlined documentation and user inputs allow users to choose any language for their orchestration wrapper \(python, c\#, java, etc\). [More info on Collibra DQ Rest APIs](https://docs.owl-analytics.com/rest-api/apis)
* Patterns
  * Fix load query generation issue when WHERE clause is specified
* Behaviors
  * Fix behavior score calculation after suppressing AR 
  * Fix percent change calculations in behavior AR after retrain
  * Mean Value Drift \[New Feature\] [Behaviors](dq-visuals/behaviors.md#using-behavioral-analytics-change-detection)
* Security
  * Introduce new role of ROLE\_DATA\_GOVERNANCE\_MANAGER with ability to manage \(create / update / delete\) Business Units and Data Concepts. [More info on Collibra DQ Security Roles](https://docs.owl-analytics.com/v/2021.08/security/owl-security/role-based-access-control-rbac)
  * Relaxed field requirements for password manager connections for App ID, Safe, and Password Manager Name
* Scorecard
  * Enhanced page loading speeds for scorecard pages
* Rules
  * Rule activity is now more efficiently parallelized across available resources
* Validate Source
  * Pie chart will highlight clearly visible ‘issue’ wedge for anything less than 100%
* UI/UX
  * Updated with more distinct icon set

## 2021.07   \(**07-09-2021\)**

_Please note updated Collibra release name methodology_

#### Enhancements

* Collibra Native DQ Connector
  * No-code, native integration between Collibra DQ and Collibra Catalog
* UX/UX
  * Full redesign of web user experience and standardization to match Collibra layout
  * Search any dataset from any page
* Hoot
  * Rules Display with \[more\] links to better use the page space
  * Auditing for changes per scan
* Explorer
  * JDBC Filter enablement by just search input
* Profile
  * Add more support for data-concepts from UI or future release
* Behaviors
  * Down-training per issue type
  * AR user feedback loop \(pass/fail\) for learning phase
* Scheduler
  * [Time based cleanup routine](https://docs.owl-analytics.com/data-retention/time-based-data-retention)
* Security
  * SQL View data by role vs just Admin
* Reports
  * OTB completeness reports from reports section. [Completeness Report](reports/completeness-report.md)

## 2.15.0   \(**05-31-2021\)**

#### Enhancements

* Hoot
  * Down-training per activity vs globally
* Logging
  * Expose server logs on the jobs page from the agent and cluster
* Explorer
  * Enhanced Experience for display of stats for database tables
  * Validation for Dupes section to ensure all input is validated before save
  * Support for edit mode with Dremio connections
  * Allow file scan skip-N to skip a number of rows if extra headers are present in the file
  * Support Livy sessions over SSL for files
* Profile
  * Add quick click rules based on profile distribution stats
* Behaviors
  * Down-training per issue type
* Scheduler
  * Support for $rdEnd in the template
  * Auto update schedule template based on last successful run
  * Support S3 custom config values in scheduled template
* Security
  * SAML Auth
  * Support for JWT Authentication to the Multi-Tenant management section
* Multi-Tenant
  * Support for an alternate display name for each tenant to be displayed in the UI and login tenant selection

## 2.14.0   \(**03-31-2021\)**

#### Enhancements

* Hoot
  * Edit mode on Password Manager supported connections
  * Edit mode on complex query
  * Behavior chart display of last 2 runs
* Explorer
  * ValSrc auto Save
  * Remote File
    * Support for Google Cloud Storage \(GCS\)
    * Support for Google Big Query
    * Folder Scans in Val Src
    * Auto generate ds name
    * FullFile for S3
    * {rd} in file path naming
    * Estimate Jobs \(Only on K8s\)
    * Analyze Days \(Only on K8s\)
    * Preview Data \(Only on K8s\)
* Connection
  * Store source name to connect a column to its source db/table/schema
  * Custom driver props for remote file connection
* Profile
  * Filtergrams for Password Manager connections
  * Filtergrams for Alternate agent path connections
  * Filtergrams on S3/GCS data source \(Only on K8s\)
* Rules
  * UX on page size options
* Scheduler
  * Support multiple db timezone vs dataset timezone
* Outliers
  * Notebook API returns true physical null value in DataFrame instead of string "null"
* Shapes
  * Expanded options for numeric/alpha
  * Expanded options for length on alphanumerics

## 2.13.0   \(**12-20-2020\)**

#### Enhancements

* Schema
  * Notify of quality issue on special characters in column names
* Shapes
  * Shape Top-N display in profile
* Behaviors
  * Chart enhancements including visible Min/Max ranges on AR drill in
  * Force pass/fail at AR item level
* Explorer
  * Menu driven selections on existing datasets
  * Run remote file scans at parent folder level
* Scheduler
  * Allow scheduling based on dataset timezone \(previously all UTC\)
* Profile
  * Enhanced Drill in display including new AR view & Shape Top-N values
  * Data Preview Filtergram Export of distinct column values
* Validate Source
  * Additional UI parameters exposed: File Type/ File Delimiter
  * Edit support in Explorer Wizard step
  * Grouped display on Hoot Page with aggregate statistics
* Business Units
  * Organize datasets by [business-units](https://docs.owl-analytics.com/observation-assignments/business-units) visible in catalog and profile views
* Hoot Page
  * Ability to Clone datasets from a given dataset run
* Rules Page
  * Allow Vertical Resize
* Catalog
  * Searchable filters for: rows, columns, scans, and more
* Performance
  * 2X faster on data loading activity based on revised caching and surrogate ID.

## 2.12.1   \(11-1-2020\)

#### Stability Enhancements

* Pattern
  * Pattern no longer overflows when too many keys are selected
  * Fix for Pattern Activity failing when no key is provided
  * Pattern now inherits its default values from the first record
* Dupe
  * Fix Dupe Case Sensitivity toggle in Wizard
* Shapes
  * Fix Shape settings being overridden
* Outlier
  * Improved validation for Outlier definition in Explorer
  * Outlier now inherits its default values from the first record
* Behaviors
  * Behaviors row count modal now correctly clears previously viewed topN and bottomN results
* Explorer
  * Fix for specifying the file type for Local and Temporary files
  * Remove hardcoded file limit of 30MB for temp files
  * Datasets can no longer be renamed in edit mode
  * Backrun is now off by default when a job is edited
  * Pattern reload now correctly displays on/off status
  * Explorer banner is now properly displayed
  * Fix for agent list not refreshing after clicking the Refresh icon
  * Fix for Analyze date field in Athena
  * Explorer now runs analyze based on transform if it is selected
  * Fix for job estimator in Athena
* Scheduler
  * Fix Kerberos authentication for scheduled jobs running on Hive
  * PwdMgr now gets connection details by tenant for scheduled jobs
  * Scheduled jobs modal now properly displays the status of the last three jobs
* Alert
  * Alert setup no longer breaks OwlCheck jobs
* Backend
  * Fix for handling reserved word 'date' in Hive.
  * Generic template is now displayed by default, even when no other connection templates have been defined
  * MIN/MAX Load Time now defaults to Off
* Install
  * Version bump and rpm style installation for a local postgres in the Owl install script

## 2.12.0     \(10-01-2020\) 

**Enhancements**

* Rule Page Builder Enhancements 
  * Native Rule Updates \(push-down\)
  * Rule Freeform Section Usability
  * Run with default Agent
* AWS S3 Role Based Authorization 
  * Leverage Instance Profile to assume a Role for authorization of S3 access
* Enable LinkID in Owlcheck Explorer 
  * Designate a column that contains a unique record identifier. The value contained in this column will be captured and stored along with DQ findings. This identifier enables data stewards to quickly find and remediate DQ findings in the source data.
* Wizard driven windowed aggregates on datasets 
  * A user can apply a SUM\(DURATION\) OVER \(PARTITION BY GRADE\)
* Bulk Delete From CatalogSecurity admin role 
  * A user can bulk delete based on time since last run, \# of total runs.
* Rule Breaks to allow for different columns 
  * A user can apply a rule that has different columns and we catch exception gracefully
* Edit OwlCheck created from CLI 
  * Allow Edit for Owlchecks initiated from CLI instead of directly from OwlDQ Explorer.
* Explorer Edit on File Data Source 
  * Ability to edit existing Olwchecks created on remote and local files. Expanded capabilities for editing Owlchecks on JDBC sources
* Edit Score Card capabilities
* Search and index dataset\_schema col in CATALOG
* Notebook API - Expanded Outliers and Patterns Results Outliers output displays 
  * Key Column names and an aggregate view that merges duplicate Outlier findings to display the number of occurrences. Patterns aggregate output denotes columns not relevant to a given finding.
* TECH PREVIEW - Kubernetes Support \(V1\) 
  * Deploy OwlDQ and run Owlchecks on Kubernetes 
* TECH PREVIEW - Streaming Owlchecks - SSL Authentication 
  * Run Streaming Owlchecks on Kafka topics protected by 2-Way SSL 
* TECH PREVIEW - Validate Source Drill-in 
  * Source activity shows more details regarding source findings. Currently view-only. Use the existing table for invalidation.



## 2.11.0     \(8-1-2020\) 

**Enhancements**

* Notebook API Enhancements
  * Support @dataset and @t1 syntax in freeform SQL for business rules
  * Multiple Outlier definitions supporting full object
  * Multiple Pattern definitions supporting full object
  * Display full rulebreak rows in output Dataframe
* Owlcheck Wizard supports multiple Outlier grouping with different keys 
  * Wizard supports definition of multiple distinct Outlier definitions using includes and keys
* Owlcheck Wizard supports multiple Pattern grouping with different keys 
  * Wizard supports definition of multiple distinct Pattern definitions using includes and keys





## 2.10.1   \(6-1-2020\)

**Enhancements**

* Scheduler Enhancements \([docs](https://docs.owl-analytics.com/scheduler/schedule-management)\)
  * Manage Schedule Restricted Times
  * Schedule Jobs By quarter
  * UX Mods on Schedule Template Save From Hoot
  * Optional Schedule Save with custom Run Date for Reporting/Charting
* Alert Enhancements \([docs](https://docs.owl-analytics.com/alerts/email-alerts)\)
  * Setup alert batches for quick distribution list and consolidated alerts per dataset
  * Configure all alerts to run via OwlWeb
* Behaviors \([docs](https://docs.owl-analytics.com/dq-visuals/behaviors)\)
  * Ability to suppress behavior items
  * UX modal enhancement for additional display values \(chart/top-N/functions\)  
* Jobs \([docs](https://docs.owl-analytics.com/apis/job-server)\)
  * Export All \(export all checkbox\)
  * Detailed logging per job \(click jobs link\)
* Scorecard Pages
  * Require Page Name
* Rules UX Enhancements \([docs](https://docs.owl-analytics.com/dq-visuals/rules)\)
  * Required/Non-Required Styling
  * Display with ellipsis on long rule names in hoot findings

**Known Issues**

* Auto Profile AGENT status indicator \(GREEN/RED\) missing
* Can not run multiple patterns or outliers from UX on Tech Preview explorer2

## 2.10.0    \(5-1-2020\)

**Features**

* Assignment Queue \([docs](https://docs.owl-analytics.com/observation-assignments/assignment-queue-s)\)
  * Assign review and resolution of data quality issues to responsible users
  * Push assignments to Service Now
* Rules Features \([docs](https://docs.owl-analytics.com/dq-visuals/rules)\)
  * Enriched Regex Builder to assist in Rule definition
* Auto Profile Phase 2 \([docs](https://docs.owl-analytics.com/dq-visuals/profile/autoprofile)\)
  * Schema filter \(option to limit fields profiled per table\)
  * Profile Pushdown \(push compute to data warehouse\)
  * Scan concurrency throttle \(limit number of simultaneous Profiling jobs\)
  * Date filter \(option to focus profiling to a date orange per table\)
* Profile UX Enhancements \([docs](https://docs.owl-analytics.com/dq-visuals/profile)\)
  * Add Business terms/descriptions to profiled columns
  * PII/MNPI designations automagically identified by Owl \(Profile Semantic\) can be removed by the user from the dataset Profile screen
  * One click to create a rule based on TopN values
* Catalog UX Enhancements \([docs](https://docs.owl-analytics.com/catalog/catalog)\)
  * List of Actions to edit/govern datasets
  * Publish Dataset
* Explorer 2 Enhancements \([docs](https://docs.owl-analytics.com/dq-visuals/explorer-2)\)
  * Support for HDFS
  * Support for ad-hoc files
* Pushdown Processing to the Data Warehouse storing the data \([docs](https://docs.owl-analytics.com/dq-visuals/profile)\)
  * Push compute of Profile to the Data Warehouse where the data is stored
  * Push compute of Validate Source to the Data Warehouse where the data is stored. Schema and Row Counts only, validate values functionality not supported when pushdown is enabled
* Outliers \([docs](https://docs.owl-analytics.com/dq-visuals/outliers)\)
  * Functionality \(Categorical Outliers\)
    * Categorical Outliers take history into account when date column is provided
    * Categorical Outliers offers visualization of Most frequent along side of the Outlier for context
  * Performance \(Numerical Outliers\)
    * Improved performance when limit on number of Outliers is increased
    * improved performance when No Date and/or Key is provided
    * Outlier key values are delimited by a user defined delimiter \(~~ by default\)
* Validate Source \([docs](https://docs.owl-analytics.com/dq-visuals/validate-source)\)
  * Improved performance when validate values function is enabled
* Behaviors \([docs](https://docs.owl-analytics.com/dq-visuals/behaviors)\)
  * Control behavior module by subtype
* Notebook API
  * option.keyDelimiter - Outlier key values are delimited by a user defined delimiter \(~~ by default\)
  * option.coreMaxActiveConnections - Maximum number of threads that an Owlcheck metastore connection pool contain. This option is only honored when the connection pool first initializes \(Typically when the Spark Session first initializes\).
  * option.profile.behaviorRowCheck - Controls if behavioral model factors in row count stats
  * option.profile.behaviorTimeCheck - Controls if behavioral model factors in load time stats
  * option.profile.behaviorMinValueCheck - Controls if behavioral model factors in min value stats
  * option.profile.behaviorMaxValueCheck - Controls if behavioral model factors in max value stats
  * option.profile.behaviorNullCheck - Controls if behavioral model factors in Null count stats
  * option.profile.behaviorEmptyCheck - Controls if behavioral model factors in Empty count stats
  * option.profile.behaviorUniqueCheck - Controls if behavioral model factors in Cardinality count stats
* Caching Efficiency
  * Improved efficiency of memory usage

**Known Issues**

* Estimate Jobs function may produce suboptimal configuration
* Kerberos Exception when attempting to generate preview for JSON/XML files on HDF
* Auto Profile AGENT status indicator \(GREEN/RED\) missing

## **2.9.0 = 4.5.2020**

**Tech preview**

* Explorer V2
  * JDBC Source Support
* Auto Profile

**Profile/Behavior**

* New Profiling Metrics and Visualizations
  * topN and bottomN
  * Types
  * Percentages
  * Visuals
* Behavior Cardinality Visuals
* AutoProfile 

**Reporting Export**

* [DQ Summary Report](https://docs.owl-analytics.com/reports/owl-summary-reports) export to various file types

**General**

* To Use `-hive` flag on hdp
  *  A separate non-jdbc hive driver package is required
  *  For assistance with this scenario please contact support.
* Rules that apply the @t1 parameter is not supported from backrun or continuous sparkOwl api

## **2.8.0 = 3.31.2020**

**Tech preview**

* Wizard 2
* Agent Native JDPC Principal/Password option
* Notebooks Multi-Pattern
* HDFS Wizard
* Qbole Integration
* Pattern Analyze

#### Behaviors

* Scoring Updates
* Item level training
* Full Automated Rules \(AR\) list exposed

**Jobs**

* Additional logging stages
* Show YARN Job Id \(If YARN Job\)

**UX: Explorer/Hoot/Profile**

* Teradata Column Based Access for preview/parallel JDBC
* HDFS Browser
* UX Enhancements to Tenant Administration
* EPV Via Agent
* Minor UX fixes/enhancements

**Reporting**

* New report section in UI will store all future OTB reports with Export

**General**

* To Use `-hive` flag on hdp
  *  A separate non-jdbc hive driver package is required
  *  For assistance with this scenario please contact support.
* Rules that apply the @t1 parameter is not supported from backrun or continuous sparkOwl api

## **2.7.0 = 1.31.2020**

**Tech preview**

*  Adaptive rules button in behavior tab

#### Multi-Tenancy

* UX Management Enhancements

**UX: Explorer/Hoot/Profile**

* Record observation keys will be delimited with \*\*\*
* Records will have key -&gt; value \*\*\* for each element
* UX Enhancements to Tenant Administration
* Remote Agent Password Manager execution
* Validate source file to file custom column selection support
* Limit capability for validate source query
* Validate source custom delimiter option

#### Setup/Flyway

* Auto-sync schema for all tenants in multi-tenancy on startup

**General**

* To Use `-hive` flag on hdp
  *  A separate non-jdbc hive driver package is required
  *  For assistance with this scenario please contact support.
* Rules that apply the @t1 parameter is not supported from backrun or continuous sparkOwl api

## **2.6.2 = 1.21.2019**

**Tech preview**

*  Adaptive rules button in behavior tab

#### Multi-Tenancy

* Added Parameter based tenant option in addition to existing Subdomain tenants

#### **Catalog**

* Ability to rename datasets via catalog page

#### **UX: Explorer/Hoot/Profile**

* Support for pre-fetch columns to fetch via JDBC driver connection
* Validate source enhancements: DB Views/ column pre-fetch
* One-click re-runs & Scheduler support for Password Manager based connections
* Re-run from hoot direct to Agent
* Profile baseline/run export JSON to csv
* \*Tech Preview: Adaptive rules listing in hoot behaviors
* Enhanced template save validation pattern for variables
* Reduce excessive notifications on behavior down-training with adjusted sensitivity

#### History/Audit

* Expanded search limit for Job History
* Exporting for activity audit
* Admin auditing for scheduled activities
* Job status cmdLine masking

#### Setup/Flyway

* Enhanced DB schema upgrade support: Upgrade from version &gt;= 2.5, install SQL script is not required
* Multi-Tenant admin support to sync schema tables plus flyway alter scripts

**General**

* To Use `-hive` flag on hdp
  *  A separate non-jdbc hive driver package is required
  *  For assistance with this scenario please contact support.
* Rules that apply the @t1 parameter is not supported from backrun or continuous sparkOwl api
* If upgrading from &lt;2.5.0 → 2.6.2, the upgrade script must be used

## **2.6.0 = 12.9.2019**

#### General

* If installing on a first time install with a clean database, you need to disable flyway with `export SPRING_FLYWAY_ENABLED=false`.
* If owl is started in a container, use the `-e` flag to add that environment variable to the container. After initialization, the application will install the schema and that flag will no longer be necessary. Flyway should be re-enabled on all subsequent starts.

#### Remote File System

* Information - RFS - Any role used to access S3 must contain the following permissions on the selected bucket \(List Bucket, Get Bucket Location, Get Object \(on the desired prefix\)
* Tech Preview - RFS - Analyze date column will not display graph
* Tech Preview - RFS - Estimate job will not estimate for remote file system
* Tech Preview - RFS - Validate source on remote file system is supported when Target dataset is a remote file system
* Tech Preview - RFS - Validate source on remote file system is not when Source dataset is a remote file system
* Tech Preview - RFS - Validate source preview and Outlier preview
* Tech Preview - RFS - Lookback preview on Explorer will not display for S3 for Outliers or Pattern sections
* Tech Preview - RFS - Owl schedule infrastructure will not work with temporary credentials
* Tech Preview - RFS - Listing contents on S3 is limited to 1000 results per directory \(Paging will be supported in future releases\)
* Tech Preview - XML Support - Deeply nested complex structures are not supported
* Not Supported - RFS - Rerunning on S3 from Hoot page is not supported
* Not Supported - RFS - Filtergram for S3 datasets is not supported
* Not Supported - RFS - S3 as a secondary rule in complex rules is not supported
* Not Supported - HDFS as a remote file system is only supported from direct command line. It is not supported as a remote file system from Explorer.

#### **Notebook API**

* Not Supported - Validate source opt.source.map is not supported

#### **Explorer**

* Update - Column selection for Dupe and Pattern sections has changed from Opt-Out to Opt-In. All checkboxes will be deselected by default for those sections in the Explorer.

## **2.5.0 = 11.15.2019**

### **Features**

* Performance enhancements for Duplicate detection
* Additional UI support in Wizard for Files
* DB Wizard Enhancements/Fixes
* Added Admin Flags for features \(catalog, logging\)
* UI Audit logging and export
* JWT AD Auth
* Parallel JDBC auto for Teradata
* Hive Recognition by Connection
* Hoot Page UI Enhancements and validation on input type \(UTF-8\)

### Change Log / Fixes

* OWL-826 Hive JDBC Kerberos User/Pass Authentication 
* OWL-639 OwlCheck All \(like Catalog All\) 
* OWL-741 How to read data from MySQL or another DataBase into a DataBricks notebook \(have to add to CP\) 
* OWL-675 This epic is to track Jira's associated with OWL notebook execution 
* OWL-921 FileQuery rewrite in Load Activity causes string case to change, breaking case sensitive queries 
* OWL-920 Add DAO for ColMatchOpt 
* OWL-919 Adding OwlOptBLL to be able to persist OwlOption \(with nested objects\) 
* OWL-914 remove unnecessary encryption initialization in Pattern Activity 
* OWL-912 Build new Model methods that expose files from S3 to the View 
* OWL-911 Build new Controller methods that expose files from S3 to the View 
* OWL-909 Remove single fields of outlier/pattern from OwlOption class 
* OWL-908 Moving fields back to OwlOption from LoadOpt 
* OWL-907 Add DAO for OutlierOpt 
* OWL-906 Enable opt\_ table creation at OwlBLL 
* OWL-905 Opt-out table creation at OwlBLL 
* OWL-904 Add Parquet, Avro, and Json file ability to Wizard 
* OWL-903 Add Multiline and Flatten to UI Wizard 
* OWL-902 Agent Log File Rollover 
* OWL-901 Research viability of obtaining customer defined ID field for each observation 
* OWL-900 OwlCheckHistoryDAO logs "No row found matching the query criteria" as ERROR, breaks hoot 
* OWL-899 jackson-databind upgrade to version 2.9.10 per CVEs 
* OWL-897 Behavioral Dimension method in Profile calls collectAsMap mutiple times 
* OWL-896 MSSQL - wizard date picker failure 
* OWL-895 DqItems.datashapes does not match data stored in metastore datashape table 
* OWL-894 Rename dataset foreign key columns to dataset\_fk 
* OWL-893 example options is not correct in the upgrade.sh 
* OWL-892 Correlation Matrix includes owl\_id column 
* OWL-891 $rdEnd Monthly Scheduler to use rdEnd 
* OWL-890 Refactor Dupe Table to Allow Overflow 
* OWL-889 Dupe Table Greater Than 200 start to break page 
* OWL-888 Refactor -rd validation to include timestamp 
* OWL-887 Removing and merging AlertOpt into OwlOpt 
* OWL-886 Removing and merging MiscOpt into OwlOpt 
* OWL-885 Show role labels with partial access and function level 
* OWL-883 Refactor Behavior Tab "NO" msg to encompass minimum number of pass runs 
* OWL-882 Catalog Runs vs Catalog with no Runs 
* OWL-877 Clean Up Dashboard Page 
* OWL-876 Add DAO for DupeOpt 
* OWL-875 Add DAO for ProfileOpt 
* OWL-874 Add DAO for SparkOpt 
* OWL-873 Add DAO for SourceOpt 
* OWL-872 Add DAO for OwlOptions 
* OWL-871 Add DAO for LoadOpt 
* OWL-870 Add DAO for PatternOpt 
* OWL-869 Add DAO for TransformOpt list 
* OWL-868 Embed SchemaOpt into OwlOpt 
* OWL-867 Graph Add Element 
* OWL-865 New TransformOpt structure 
* OWL-864 Move all fields from TransformOpt to LoadOpt 
* OWL-856 avro, hdfs, parquet files for filtergram 
* OWL-854 Add DAO for EnvOpt 
* OWL-853 Add DAO for SchemaOpt 
* OWL-852 Add DAO for RecordOpt 
* OWL-848 \[Tech Debt\] How to add 'dataset' field as named parameter where table doesn't have this column 
* OWL-847 Adding DAO for RuleOpt 
* OWL-839 Implement user defined NullValue replacement for Parquet 
* OWL-833 Model method to enable Kerberos User/Pass Prompt Authentication Connection Type 
* OWL-831 Add to controllers for file wizard for parquet and avro 
* OWL-823 Store/Update and show profile image on profile page 
* OWL-822 Profile user image storage support on controller and db 
* OWL-821 Aggregate timestamps on scope view to day 
* OWL-819 Bulk delete option for removing datasets from Catalog page 
* OWL-813 Prep Sample Data Files 
* OWL-812 Updated security documentation on new roles and ACLs 
* OWL-808 \[Tech Debt\] Instantiating \*\*Opt fields only if there are any changes in default values 
* OWL-802 patterns showing observations for mismatch soucre and schema 
* OWL-798 Char conversion in db2 - recreate to fix 
* OWL-797 Test cases for role mappings 
* OWL-796 Allow dynamic setting for UI timeout in JS 
* OWL-791 Auto mapping of Roles Disabled by default 
* OWL-785 Configure JWT token duration via props 
* OWL-784 Store JSESSIONID and USER IP in log output 
* OWL-783 Adding TransformOpt and mapping 
* OWL-782 Extending SparkOpt and mapping 
* OWL-781 Extending SourceOpt and mapping 
* OWL-780 Adding SchemaOpt and mapping 
* OWL-779 Extending RuleOpt and mapping 
* OWL-778 Adding RecordOpt and mapping 
* OWL-777 Recheck usage of N/A marked properties 
* OWL-776 Extending ProfileOpt and mapping 
* OWL-775 Extending PatternOpt and mapping 
* OWL-774 Extending OwlOptions and mapping 
* OWL-773 Extending OutlierOpt and mapping 
* OWL-772 Extending LoadOpt and mapping 
* OWL-771 Adding EnvOpt with mapping 
* OWL-770 Extending DupeOpt and mapping 
* OWL-769 Adding AlertOpt with mapping 
* OWL-768 JWT AD With Special Char Passwords 
* OWL-767 Logs that roll don't have the same permissions as the original 
* OWL-765 Working owlcheck command line example 
* OWL-763 Store login/logout information in PG 
* OWL-760 Flyway - DB migration between version of software 
* OWL-759 OPT\_LOAD, OPT\_OUTLIER, OPT\_all9tabactivities 
* OWL-750 Behavior page \(pie char\) hitting getprofiledeltasbyrunid shows 500 
* OWL-733 DB Notebook execution against a DB that is not Postgres 
* OWL-706 Outlier limits are not enforced for categorical outliers 
* OWL-687 Show the time when an owlcheck was kicked off in the UI 
* OWL-662 Build new Controller methods that expose files from HDFS to the View 
* OWL-661 Build new Model methods for Owl Web to Enable access to HDFS 
* OWL-660 Expand File Explorer to achieve functional parity to JDBC Explorer 
* OWL-638 User Profile Page with rich features 
* OWL-627 Global Connection Stops working after a few days 
* OWL-625 Automatic Scan of entire Database near Catalog on Explorer 
* OWL-597 Handle File Charset Encoding other than UTF-8 
* OWL-562 Data preview on hoot page with masking checkboxes in header 
* OWL-531 Documentation on Profile page 
* OWL-513 Refactor Owl Notebook API to make History loading conditional 
* OWL-506 props.datasetSafety = false; not working from a DB notebook 
* OWL-496 Databricks cluster job succeeds from owl standpoint but the job fails from DataBricks standpoint 
* OWL-359 Column level masking on data preview 
* OWL-884 Add Unicode to the Wizard Builder 
* OWL-599 Discover that target file is encoded as something other than UTF-8 in Explorer 
* OWL-973 Default initial scorecard page 
* OWL-971 Spinner on barchart load after date selection \(ScopeTab\) 
* OWL-959 App Props for DB Logging on auth and page acceess 
* OWL-945 "Get Started" tab of Explorer on DB connection does not present a form to edit dataset name or date 
* OWL-927 Wizard should inject schema.tablename for default query when building Owlcheck for Hive/Impala datasource 
* OWL-917 PWD masking in job status page 
* OWL-851 Modify Connection page to include a check box called "Hive Direct Eligible" 
* OWL-849 Add Auto Parallel JDBC support for Teradata 
* OWL-846 Manual override of Parallel JDBC partitions on Wizard Parallel JDBC tab 
* OWL-820 Double code mirror on Explorer \(See Attached\) 
* OWL-686 Default settings for show Views and Stats in Explorer OWL-941 Login/Logout/User Interaction DB Logging 
* OWL-939 Fix Validate Source Inputs 
* OWL-929 User Audit UI Page with Export 
* OWL-928 Add -df dateFormat option for file wizard 
* OWL-915 Force UTF-8 Chars in owlcheck 
* OWL-881 MT OwlHub require admin user/pwd to be set 
* OWL-976 Refactor Connections Screen on Click Logic for Form 
* OWL-975 Refactor Dataset Scope Blocker 
* OWL-974 Make Connection URL Input on keyup change 
* OWL-972 Refactor Explorer Dataset Scope Click Change Event on Where Clause 
* OWL-963 parallell on: -column not there 
* OWL-962 Add Promise before Impact Btn logic 
* OWL-960 Catalog Search Ranked Order by RUNs 
* OWL-958 Adding upsert method to PatternOptDao by ID field 
* OWL-957 Adding upsert method to OutlierOptDao by ID field 
* OWL-946 When Date is present in the where clause, Wizard adds TO\_DATE\(\) function even when database is not Oracle 
* OWL-944 Validate Source with Oracle as source or target adds TO\_DATE\(\) to predicate of both source and target. 
* OWL-940 -srcq displays the incorrect selection 
* OWL-936 Multiple OwlCheck Command Lines 
* OWL-932 Adding unit tests to check each \*Opt. mapping 
* OWL-930 Enable LinkId capture and storage for Rules 
* OWL-922 Customer Defined LinkId on Observations/Outliers/Shapes/Rules 
* OWL-916 Changing Estimates in Wizard 
* OWL-910 Connections Page don't allow spaces in Alias Name 
* OWL-866 VS Support DB to file and file to DB 
* OWL-850 Modify Load activity to parse props.columnname to determine partition calculation aggressiveness 
* OWL-938 Track Hoot Page Tab with Darker Color
* OWL-937 Refactor Left Nav

### **Known Issues**

* Wizard Key selection without column inclusion
* UI Audit time in UTC
* Jobs Page Limit to 120
* Wizard "Check" All by Database Button is in Tech Preview

### Miscellaneous

1. If running on agent, make sure the directory that stores you driver jars is mapped to the exact location stored in the web.

   Web: -lib /opt/owl/drivers/oracle/

   Agent: -lib /opt/owl/drivers/oracle/

   \[agent directory structure needs to map exactly to the web connection directory structure\]

2. Reduced sensitivity of Load Time behavior detection
3. Different locations for Explorer and Connection in blue navigation panel
4. Explorer Expands to Full Screen upon entering dataset scope tab

**Notebook API**

1. opt.source.map map is not available in Notebook api
2. Cluster restart required when adding nodes to re-initialize static app configs.
3. if opt.outlier.on = true and not using Owl Load\(\) to load dataframes, dfHist.createOrReplace\("historical"\)
4. If opt.pattern.on = true, pattern needs a date column to run \(-adddc -fpgdc OWL\_RUN\_ID or define -fpgdc as actual date column\)
5. spark.catalog.clearCache\(\) should be called to clear rdd storage \(rdd build-up can occur if not routinely clearing legacy cached rdds\)
6. LinkId should be a unique row identifier

## **2.4.2 = 10.2.2019**

### Features

* Bug Fixes

### Change Log / Fixes

* OWL-732 Owl.owlCheck\(\) fails if props.cardOff set to true 
* OWL-743 Add test notebook on DataBricks 
* OWL-730 Cover Dupes activity with test notebooks on DataBricks 
* OWL-744 Cover Profile activity with test notebooks on DataBricks 
* OWL-742 Add ATM test notebooks on DataBricks 
* OWL-701 long running fpg - review fpg buckets - not adhering to 50k limit 
* OWL-681 Catalog hangs from spark where 1 =0 wrapper 
* OWL-431 Additional User Activity Logging 
* OWL-626 Create DATA\_PREVIEW role to control who can see stored customer data 
* OWL-735 When filequery is enabled, data is cached but then dropped from memory before Profile

### **Known Issues**

* Validate Source if Oracle is Target TO\_DATE is applied and breaks  -- work around remove TO\_DATE from Source  -- impala and certain databases that do not support TO\_DATE
* Back run -br does not warn you that ${rd} does not exist on wizard
* ~\| as a file delimiter does not work in the UI \(works via OwlCheck\)
* Estimate Job does not always take. You can only click it while on Config Tab first
* Patterns large data long compute cycle
* If Run Date doesn't match to where clause date you run the risk of misaligned data, most notably in outliers and FPG
* Job Scheduler start time is based on JVM start.  If time is set to start job at 12:00:00 it may start at 12:00:59 if the JVM started on the 59th second.
* Agent Edit page doesn't allow for edit of script location or name.
* Creating a tenant will need an admin to login and sync schema after creating \(should be done immediately after creation\).
* Job Estimator will be enhanced with additional parameters to generate more accurate estimates
* postgres username cannot contain a "-" during setup
* password with a $ in it need to be escaped

## **2.4.0 = 9.25.2019**

### **Features**

* Use-ability / bug fixes
* Enhanced scheduler
* Wizard improvements parallel JDBC in wizard

### Change Log / Fixes

* OWL-542 Wrong initial Score calculation 
* OWL-621 DQ INBOX Refactor and LIST VIEW 
* OWL-659 Modify Owl Web to store and handle Spark enabled Principals and JDBC enabled Principals separately 
* OWL-351 Document DB Encryption Requirements Per Type 
* OWL-549 Build OwlHub Metastore and DAOs 
* OWL-585 MT - new install no tables and the export MULTITENANTMODE=TRUE doesn't create main tables 
* OWL-629 MT Login Via AD 
* OWL-510 DB Notebook issue - Dataset score shows double reduction in the UI. 
* OWL-665 Web UI should expose shape sensitivity and column exclusion settings on the Shapes tab on Hoot page 
* OWL-623 SENSITIVIY PopUp 
* OWL-160 setup.sh better handling if packages are not included in the package directory 
* OWL-664 Populate executor cores field using values returned by job estimator 
* OWL-622 SEARCH for PROFILE and HOOT in 1 
* OWL-548 POC Run multiple tenants by schema in parallel 
* OWL-667 Implement Web Controller method to write Shape settings to metastore 
* OWL-700 sensitivities reduced for nulls empties and mixed types 
* OWL-624 REPORT Summary View for public roles 
* OWL-666 Data Shapes Noise Reduction Phase 2 
* OWL-630 JWT MT Testing multi login scenarios 
* OWL-586 Cannot log into to MT enabled UI trying owlhub 
* OWL-511 DB notebook error in UI. UI shows 1 column added no matter what dataset I run against 
* OWL-708 Fix CMD wrap 
* OWL-707 Validate CMD to throw error when no 'TO\_DATE' for Oracle 
* OWL-652 dlexc dlinc added for categorical outliers 
* OWL-532 Documentation on SQL Editor
* OWL-263 Implement Kerb Principal and Keytab handling in Owlcheck 
* OWL-572 AD Auth Providers Per Tenant 
* OWL-658 Expand Owlcheck to handle multiple Principals/Keytabs for different purposes 
* OWL-498 Test Case - Match All Hoot Components for FPG and Validate Source to Hoot BLL and Sub Scoring Components to Scores BLL 
* OWL-691 Handle Web UI for endpoints that return a 403 for no Data Preview Access 
* OWL-690 Refactor Hoot Page Permissions for DATA\_PREVIEW Role 
* OWL-657 Kerberos Connect-As for JDBC connections 
* OWL-693 Upload File to Rule Truthset OWL-618 HOOT job ERROR MSG display 
* OWL-689 opts doesn't seem to have pguser/pgpassword or host parameters 
* OWL-656 Establish Secured HDP 3.1 cluster for testing 
* OWL-613 datashapescore flag is not being honored 
* OWL-698 dupe first character as 0 fixed 
* OWL-620 Data Preview TYPES in header vs LABELS 
* OWL-695 Validation for Truthset Forms 
* OWL-694 Concat Columns for Categorical Outliers 
* OWL-619 Catalog +/- to arrow 
* OWL-696 Add run tab to Rule page to re-run owlcheck with rules 
* OWL-563 MT Documentation 
* OWL-565 Logging validation 
* OWL-562 Data preview on hoot page with masking checkboxes in header 
* OWL-647 Exclude columns from Shape discovery in Owl Core 
* OWL-604 MT - trying to execute a job to a specific agent throws an error 
* OWL-682 Datashape table is not being cleared when re-running a existing day 
* OWL-530 Documentation on Rules - update the rules section of docs 
* OWL-648 Auto configure Shapes Sensitivity 
* OWL-411 UI display of estimation details on wizard 
* OWL-410 Job resource requirement calculation 
* OWL-684 Sample 10 examples of Shapes Data Preview Highlights 
* OWL-610 Testing validate source from UI 
* OWL-685 Bin Month By Month fix date parsing 
* OWL-553 Stress Test Concurrent tenant logins 
* OWL-552 "Web Scheduled Tasks by Schema \(cache job schedule\)" 
* OWL-632 Refactor Outlier History and Preview 
* OWL-555 Owl setup with option to enable multi tenant with app props 
* OWL-554 Owlcheck web custom -h flag if MT enabled 
* OWL-362 Documentation user setup on all three encryption options 
* OWL-361 Create new table/DAO/Domain Object for Col Masking 
* OWL-209 New log4j2.xml file changes the owlcheck parameters 
* OWL-593 MT with the use of agents 
* OWL-671 Misleading example/hint SQL statements on Rule -&gt; FreeformSQL -&gt; SQL Editor page 
* OWL-715 "Hive emits columns formated table.colum breaks ValSrc auto mapping" 
* OWL-557 JWT/Cookie CURL in multi tenant mode 
* OWL-439 New dataset runs do not show schema labels 
* OWL-633 explorer wizard &lt;= replaces with &gt;= 
* OWL-515 regular -dl outlier \(take outlierLimit\) cap data preview inserts 
* OWL-559 Default configuration of tenant admin on enable MT 
* OWL-635 file explorer wizard \(local file don't add yarn parameters\) 
* OWL-558 Alt login path if entering owl hub 
* OWL-676 Inject Kerberos Principal and Keytab required to submit Owlcheck via agent configs 
* OWL-678 Hive -jdbcprinc -jdbckeytab patch 
* OWL-673 Shape DataPreview Batch Insert fails if preview row column value is NULL \(DB NULL constraint\) 
* OWL-479 Run OwlCheck Cluster mode when Hive JDBC is the Source 
* OWL-600 "Handle Tab and ""~\|"" delimiter for file ingest in Owlcheck" 
* OWL-674 MIN/MAX stats = NULL causes NPE in Histograms

### **Known Issues**

* Validate Source if Oracle is Target TO\_DATE is applied and breaks  -- work around remove TO\_DATE from Source  -- impala and certain databases that do not support TO\_DATE
* Back run -br does not warn you that ${rd} does not exist on wizard
* ~\| as a file delimiter does not work in the UI \(works via OwlCheck\)
* Estimate Job does not always take. You can only click it while on Config Tab first
* Patterns large data long compute cycle
* If Run Date doesn't match to where clause date you run the risk of misaligned data, most notably in outliers and FPG
* Job Scheduler start time is based on JVM start.  If time is set to start job at 12:00:00 it may start at 12:00:59 if the JVM started on the 59th second.
* Agent Edit page doesn't allow for edit of script location or name.
* Creating a tenant will need an admin to login and sync schema after creating \(should be done immediately after creation\).
* Job Estimator will be enhanced with additional parameters to generate more accurate estimates
* postgres username cannot contain a "-" during setup
* password with a $ in it need to be escaped

## **2.3.0 = 8.30.2019**

### **Features**

* Multi Tenancy 
* Masking
* JWT CURL

### Change Log / Fixes

* OWL-566 Outliers Performance Review 
* OWL-522 Rules UI refactor 
* OWL-528 Build Controller method that determines whether there is a minority set of data shapes and only returns those shapes 
* OWL-605 profileRDD for comparison 
* OWL-550 OwlHub Management GUI for Multi Tenancy
* OWL-524 behavior dimension to check for nulls 
* OWL-567 Shapes Insert unique idx conflict fix 
* OWL-603 Lookback query does not build correct bin boundaries 
* OWL-526 Handle Data Shapes more efficiently both for user experience and backend processing 
* OWL-590 Turn Outliers Preview Highlight back on with bulk write to DB 
* OWL-587 Load Activity does not correctly build time binned historical queries for PG/Oracle/MSSQL/DB2 
* OWL-608 validate source matches and counts 
* OWL-589 Specifying a queue name in the explorer page on the config tab doesn't get added to the ""Run CMD"" owlcheck cli
* OWL-594 Installing just owl agent doesn't prompt for owl-postgres password 
* OWL-595 Agent Configs number of cores doesn't get added to the owlcheck 
* OWL-556 Customize Login page to select tenant before login 
* OWL-592 Compute Stats in DQRowCheck routine to optimize Profile Activity 
* OWL-614 Don't down score for Schema Evolution on first run 
* OWL-591 MultiTenant \(MT\) creation of more then one tenant spawns duplicates 
* OWL-598 Enable core to handle non-UTF-8 encoding when parsing target and source files 
* OWL-600 "Handle Tab and ""~\|"" delimiter for file ingest in Owlcheck" 
* OWL-596 setup.sh when only installing Postgres misses creation of owl-env.sh script 
* OWL-545 setup.sh script all parameterized for unattended installations of owl 
* OWL-130 Agent Documentation
* OWL-607 dupe test for block index 
* OWL-606 validate source matching values with count  
* OWL-576 Integrate BitBucket with Jenkins to automatically build and test batches of commits 
* OWL-134 MultiTenancy Documentation 
* OWL-133 HA Documentation

### **Known Issues**

* Job Scheduler start time is based on JVM start.  If time is set to start job at 12:00:00 it may start at 12:00:59 if the JVM started on the 59th second.
* Agent Edit page doesn't allow for edit of script location or name.
* Creating a tenant will need an admin to login and sync schema after creating \(should be done immediately after creation\).
* Job Estimator will be enhanced with additional parameters to generate more accurate estimates
* postgres username cannot contain a "-" during setup
* password with a $ in it need to be escaped

## **2.2.1 = 8.23.2019**

### No Features

* Bug fixes only

### Change Log/Fixes

* Performance related improvements.  
* Bulk inserts into owl-postgres metastore

## 2.2.0 = 8.12.2019

### **Features**

* Improvements in DataBricks integration
* SQL Editor
* Explorer Page usability enhancements

### Change Log/Fix

* OWL-544 Datasets with a high number incidents of shape issues align all rows in preview 
* OWL-541 Create Additional Estimate Button on Explorer to display row and col values in addition to  run settings 
* OWL-539 Implement Logic for runDate on owlCheck 
* OWL-538 Performance tuning of Histogram String when low number of rows and high number of columns 
* OWL-536 datashapes drill in with preview update
* OWL-535 template creation with $rd parameter support. 
* OWL-534 Break Load\(\).execute\(\) into modular methods to better control loading and caching 
* OWL-533 change setup.sh script to pull hostname and add to owl-env.sh in place of localhost 
* OWL-527 Only look for data shapes on columns that have not been tagged as a semantic schema type 
* OWL-523 Dupe Slider in Wizard 
* OWL-521 VarSrc Lib in wizard owlcheck 
* OWL-520 Add Data Preview Collapsible Area Above Agent Area on Explorer 
* OWL-514 Owl Notebook API support for loading historical data 
* OWL-512 master - UI explorer adding custom persist at runtime. 
* OWL-504 256Bit Encryption on internal Enc Method 
* OWL-503 log encryption for Spark UI 
* OWL-502 Agent add exports in owl.properties specifically for agent due to shade of postgres 
* OWL-501 Clean Activity fix \(VizErrors.Clean\(\) test case fix\) 
* OWL-500 Load Phase Build Historical breaks when dataCol predicate comes after where statement 
* OWL-497 Alter table commands between versions of owl - \(Postgres release\) 
* OWL-495 Databricks notebook execution have to manual update the application.properties file for it to write back to DB 
* OWL-494 Hoot Page Always Show 'Processing' for Hourly and Minute Run Ids 
* OWL-493 2019-06-18T11:08:00.000 0000 Date Parser Format Support 
* OWL-488 Categorical Data Preview Inserts - Check for Accuracy 
* OWL-484 Test Rules for Notebook API per OWL-472 
* OWL-483 --Conf support at CmdLine 
* OWL-481 Wizard Kerb Hive Support for OWL-479 
* OWL-480 Kerb JDBC Connection for OWL-479 
* OWL-479 Run OwlCheck Cluster mode when Hive JDBC is the Source 
* OWL-466 UI Save enhanced notifications
* OWL-451 Run Tab enhancements In Wizard 
* OWL-437 Hoot DataPreview Highlight and Shapes 
* OWL-406 UI Global connection with customer password manager option 
* OWL-390 more s3 test cases 
* OWL-346 Hoot dynamic loading with UI improvements 
* OWL-322 Truth Set Rules 
* OWL-98 Install of components, interaction base on what is NOT installed. 
* OWL-48 COLUMN SEARCHING IN WIZARD

### **Known Issues**

* Job Estimator will be enhanced with additional parameters to generate more accurate estimates
* postgres username cannot contain a "-" during setup
* password with a $ in it need to be escaped

## 2.1 = 7.18.2019

### Features

* Scheduler added
* Support for XML/ORC
* Disable/Enable Notebook & Orient features for the UI
* Admin Delegate sub-authorities for Managing User Access to Various Functions 
* owlcheck support of --conf \(in owl-env.sh\)
* Connection Templates for common drivers

### **Change Log/Fix**

* OWL-453 Reference Record for Record Added Dropped
* OWL-285 rule history -&gt; removeAllRules, 
* OWL-486 Dupes on an integer column causes dupes to NOT be found, 
* OWL-460 owlcheck examples on gitbook, 
* OWL-459 documentation: add information about the scheduler \(screenshots\) and how to use it.,
* OWL-457 backrun \(-br\) using cluster mode is failing do to what seems to be a spark context issue,
* OWL-446 Any time the timezone is updated it generates more behaviors, 
* OWL-445 Setup.sh script to include all drivers at install time, 
* OWL-426 OwlCheck cannot run in Cluster mode when Hive JDBC is the Source, 
* OWL-423 Postgres Multiple Schema test within the same DB, 
* OWL-387 If Alert mail server is not setup - alert user when the click alerts that no email server has been setup
* OWL-386 If Orient or Zeppelin are not installed we should just remove the buttons from the UI
* OWL-344 owlcheck support of --conf
* OWL-476 DataPreview Working in Hoot but not Rules/Profile
* OWL-468 Databricks - Classpath issues running notebooks
* OWL-467 Upgrade Web/Common to Spring 2 
* OWL-465 Application Features Endpoint
* OWL-464 Controller Endpoint for Update Agent
* OWL-462 Edit Agent Modal
* OWL-461 Page Running status for Notebooks and Orient on Load
* OWL-455 Shapes Testing
* OWL-454 Hoot Actions Tab Updates
* OWL-452 Pattern - rebranding and usability in explorer
* OWL-450 Connection Templates For Common Drivers
* OWL-449 Scheduler - one click Job scheduling
* OWL-447 Back running - replays with templates
* OWL-441 Job Scheduling 
* OWL-435 Shapes drill in preview does not scroll horizontal
* OWL-433 Batch insert for DAO DataPreview by Executor
* OWL-430 Change support email address
* OWL-400 Validate Passfail limit &lt; 75 fails runs
* OWL-393 Application Status Endpoint
* OWL-25 Owlcheck on XML file format
* OWL-24 Owlcheck on ORC file format
* OWL-469 Agent New Default values
* OWL-456 JOB UserName
* OWL-349 Alert Form Validation
* OWL-487 Add Hive Warehouse Connector to support "Hive Native" on HDP3.x
* OWL-485 Support Owlcheck on XML files
* OWL-473 Outlier Binned Timeseries \(HOUR/MIN\) does not calculate correct time range \(startdate time missing\), 
* OWL-472 Migrate Notebook API to use Load activity 
* OWL-470 Use New DAO batch methods to better control Shapes Issues written to metastore,

### **Known Issues**

* Job Estimator will be enhanced with additional parameters to generate more accurate estimates
* postgres username cannot contain a "-" during setup
* Agent logic has issues with shaded jar \(com.owl.org.postgresql.Driver\) that is rectified in next version OWL-501.

## 2.0 = 6.27.2019

### Features

* Encryption at REST 
* Job Status Page
* Rules Src Validate Function
* Explorer search and custom filters
* Profile and Hoot UI Enhancements
* New App props [\(see all\)](https://app.gitbook.com/@owl-analytics/s/user-guide/installing#configuration-env-settings-within-owl-env-sh)
  * Key 2.0 Additions for custom configuration of the meta-store DB in owl-env.sh:
    * SPRING\_DATASOURCE\_URL
    * SPRING\_DATASOURCE\_USERNAME
    * SPRING\_DATASOURCE\_PASSWORD
  * Matching configuration properties for owlcheck in owl.properties
    * spring.datasource.url
    * spring.datasource.password
    * spring.datasource.username

### **Change Log/Fix**

* OWL-292 Create Agent Component on Wizard Page 
* OWL-293 Refactor Owlcheck submission for agent/agent\_group as agent and agent\_group use Serial/Integer 
* OWL-294 LOG Files CLUSTER Mode 
* OWL-296 Spark options \(bounds/colname/partition\) 
* OWL-298 Owl-env.sh script use Lib option 
* OWL-303 Cloudera Test Env Setup 
* OWL-304 Rules Refactor Speed Increase 
* OWL-305 Rules Score Update 
* OWL-306 Cloudera Env infrastructure support 
* OWL-307 Rules HOOT shows \(5\) when nothing breached 
* OWL-309 Job Status . FINISHED, RUN ALL in UI table 
* OWL-310 Rule page to use a runId for toggling 
* OWL-311 Profile Page to Use new Datapreview and Histogram expand fullscreen 
* OWL-312 Current date selected in hoot page heatmap chart \(top chart \#2\) not showing for long runId 
* OWL-313 Profile Page Rework all sections 
* OWL-314 null in filtergram check and replace with string 'null' 
* OWL-315 cascading and repeating names in scorecard page 
* OWL-317 Spark Tuning R&D 
* OWL-323 Rules Current vs Last Run \(t1\) usability enhancement 
* OWL-334 Rules Performance 
* OWL-336 Rules UI Error Handling 
* OWL-337 Rules CodeMirror Syntax Validation 
* OWL-338 Item labels on behavior items 
* OWL-340 Application User Logs 
* OWL-341 AgentQ Table for issuing agent job requests 
* OWL-342 Job Status Page Enhancements for all owlChecks 
* OWL-345 Ability to change all default passwords \(such as orient/postgres\) 
* OWL-350 HOOT TimeZone Edit button 
* OWL-356 Security Configuration option for type of encryption to be used 
* OWL-357 Configuration Setting for where to get public encryption key for encryption/decryption 
* OWL-363 HOOT Processing outlier...dupe... 
* OWL-364 Jenkins Build process / Test invoke / email on failures 
* OWL-365 Filter options for JDBC query before expanding the DB 
* OWL-366 owlcheck overwriting the semantic schema issue 
* OWL-370 Dupe Detection runtime reduction 
* OWL-371 Activity Decouple 
* OWL-372 Hist refactor for performance 
* OWL-373 WebApp Driver UnRegister Bad Driver 
* OWL-375 Load Time Trigger 
* OWL-378 Datashape Distribution turn back on, profile the performance issue 
* OWL-379 Retrain Button 
* OWL-380 RECORD Changes and SCHEMA Changes not showing in UI 
* OWL-381 HOOT timezone says TRUE 
* OWL-382 Item Label Outlier 
* OWL-383 Install and test v2.0 of Owl with Postgres version 9.6.5 
* OWL-384 Encrypt data within postgres Data\_Preview table \(decrypt automatically\) 
* OWL-385 dataset\_field table encryption using java encryption key held in owl 
* OWL-388 encryption of the dataset\_field\_value table 
* OWL-389 dataset\_hist table doing columns hist\_values 
* OWL-395 ItemLabel table encryption of column item\_values 
* OWL-396 Explorer RUN Tab UI 
* OWL-397 Load Time Alert 
* OWL-398 ReTrain Changes Score on behavior item for previous runs 
* OWL-401 DuplicateLabels added anytime I down train an item 
* OWL-402 observation table - encrypted \(out\_column, out\_value, out\_median\) 
* OWL-403 outlier table encryption at rest in postgres 
* OWL-404 Once you label something as ignore it cannot be set back to - not be ignored 
* OWL-413 Owl web app fails to restart with error below 
* OWL-414 -h command doesn't work with owl-core if not using the default schema name in Postgres 
* OWL-416 Hive JDBC connection in Explorer page 
* OWL-417 Remove HBase Phoenix 
* OWL-418 Data Cleanup Thread 
* OWL-419 PG Connections encryption pwd 
* OWL-420 PG Credentials in props and Batch Insert for Executor Insert Model 
* OWL-421 Oracle mod to filtergram needs wrapper for rownum where clause limit 
* OWL-422 Filtergrams with Oracle not working \(SQL Exception: Unable to execute sql for this dataset\) 
* OWL-424 Add agent start/stop to owlmanage.sh 
* OWL-425 val src observations inserts 
* OWL-427 Audit Trail Timestamp conversion from epoch long to a readable date 
* OWL-428 Performance improvements 
* OWL-434 Cleanup/Constraint options for insert Data Preview 
* OWL-444 DevOps - Setup script doesn't interrogate user for orient password at setup 
* OWL-466 UI Save with no success/failure response back to user 
* OWL-471 Ensure valsrcinc/valsrcexc columns are applied to schema checks and counts

### **Known Issues**

* Default notification email "To" email address is not customizable

