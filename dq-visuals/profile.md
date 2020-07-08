# Profile

## Automatically Profile

Owl automatically profiles datasets over time to enable drill-in for detailed insights an automated data quality. A profile is just the first step towards an amazing amount of auto discovery. Visualize segments of the dataset and how how the dataset is changing over time.

## Dataset Profile

Owl creates a detailed profile of each dataset under management. This profile will later be used to both provide insight and automatically identify data quality issues.

{% hint style="info" %}
Owl can compute the profile of a dataset either via Spark or the Data Warehouse where the data lives as the engine. The following DBMS systems are supported for "Profile Pushdown"

* Impala 
* Hive 
* Snowflake 
* Presto 
* Teradata 
* SQL Server 
* Postgres 
* Redshift 
* Mysql 
* Oracle 
* DB2 

When the Profile is computed using the datasource DBMS, TopN visualization is not computed.
{% endhint %}

![](../.gitbook/assets/screen-shot-2020-05-07-at-7.28.25-pm.png)

## Profile Insights

![](../.gitbook/assets/screen-shot-2020-05-07-at-7.33.16-pm.png)

By gathering a variety of different statistics, Owl's profile can provide a great deal of insight about the dataset.  

{% hint style="info" %}
Profile includes a range of statistics

* Actual Datatype
* Discovered Datatypes
* Percent Null
* Percent Empty
* Percent Mixed Types
* Cardinality
* Minimum
* Maximum
* Mean
* TopN / BottomN
* Value Quartiles
{% endhint %}

## Correlation Matrix

Discover hidden relationships and measure the strength of those relationships.

![](../.gitbook/assets/owl-relationships.png)

## Histograms

Often the first step in a data science project is to segment the data. Owl automatically does this using histograms.

![](../.gitbook/assets/owl-histogram.png)

## Data Preview

After profiling the data, for those users with appropriate rights, Owl provides a glimpse of the dataset. The Data preview tab also provides a some basic insights such as highlights of Data Shape issues and Outliers \(if enabled\), and Column Filtergram visualization.

![](../.gitbook/assets/screen-shot-2020-05-07-at-7.57.29-pm.png)



