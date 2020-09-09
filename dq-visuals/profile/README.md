# Profile

## Automatically Profile

Owl automatically profiles datasets over time to enable drill-in for detailed insights an automated data quality. A profile is just the first step towards an amazing amount of auto discovery. Visualize segments of the dataset and how how the dataset is changing over time.

## Dataset Profile

Owl creates a detailed profile of each dataset under management. This profile will later be used to both provide insight and automatically identify data quality issues.

![](../../.gitbook/assets/screen-shot-2020-07-08-at-12.45.19-am.png)

Owl can compute the Profile of a dataset either via Spark \(No Pushdown\) or the Data Warehouse \(Profile Pushdown\) where the data lives as the engine. When the Profile is computed using the datasource DBMS the user can choose two levels of pushdown: 

* Full Profile - Perform full profile calculation except for TopN 
* Count - Only perform row and column counts

{% hint style="info" %}
The following DBMS systems are supported for "Profile Pushdown"

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
{% endhint %}

![](../../.gitbook/assets/screen-shot-2020-05-07-at-7.28.25-pm.png)

## Profile Insights

![](../../.gitbook/assets/screen-shot-2020-05-07-at-7.33.16-pm.png)

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

## Sensitive Data Detection \(Semantic\)

Owl can automatically identify any types of common PII columns. 

{% hint style="info" %}
Owl is able to detect the following types of PII

* EMAIL
* PHONE
* ZIP CODE
* STATE CD
* CREDIT CARD
* GENDER
* SSN
* IP ADDRESS
* EIN
{% endhint %}

![](../../.gitbook/assets/screen-shot-2020-07-08-at-12.37.10-am.png)

Once detected, Owl will tag the column in the Profile as the discovered type as well as automatically apply a rule. If the user can choose to decline any discovered tag by simply clicking on it and confirming the delete action. This action can also remove the rule associated with the tag.

![](../../.gitbook/assets/screen-shot-2020-07-08-at-12.39.13-am.png)

## Correlation Matrix \(Relationship\)

Discover hidden relationships and measure the strength of those relationships.

![](../../.gitbook/assets/owl-relationships.png)

## Histograms

Often the first step in a data science project is to segment the data. Owl automatically does this using histograms.

![](../../.gitbook/assets/owl-histogram.png)

## Data Preview

After profiling the data, for those users with appropriate rights, Owl provides a glimpse of the dataset. The Data preview tab also provides a some basic insights such as highlights of Data Shape issues and Outliers \(if enabled\), and Column Filtergram visualization.

![](../../.gitbook/assets/screen-shot-2020-05-07-at-7.57.29-pm.png)



