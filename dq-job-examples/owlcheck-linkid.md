# OwlCheck LinkId

Ability to link an OwlCheck findings back to the source record for remediation.  The linkId needs to be unique, commonly the primary key.  There are 2 ways to provide the linkId, 1\) a the cmdline via -linkid or 2\) in a notebook via opt.linkId.  Owl supports one or many primary key columns in your datasets for record linkage to your original table, file or dataframe.  If your primary key column contains many columns use a comma to delineate.

### Notebook

```scala
val opt = new OwlOptions()
opt.runId = "2018-02-24"
opt.dataset = "orders"
opt.linkId = Array("transaction_id", "trans_time")
```

### CmdLine

```bash
./owlcheck -ds orders \
-rd "2018-02-24" \
-linkid transaction_id,trans_time 
```

### Activity Usage

| **Activity** | **Supported** | **Description** |
| :--- | :--- | :--- |
| **SHAPE** | YES | 1 Example of each shape issue will have a link back to the corrupt record for remediation. |
| **OUTLIER** | YES | Each outlier will have a link back to the detected record for remediation.  If you apply a limit you will only get the limited amount. Not on categorical. |
| **DUPE** | YES | Each duplicate or fuzzy match will have a link back to the record for remediation. |
| **SOURCE** | PARTIAL | Each source record that has a cell value that doesn't match to the target will have a link for remediation.  SOURCE will not have links for row counts and schema as these are not record level findings. |
| **RULE** | YES | Break records for Freeform and Simple rule types will be stored \(any records that did not meet the condition of the RULE will be provided with the linkId columns\).  These are stored as delimited strings in the rule\_breaks table along with the dataset, run\_id and rule name.  Please note when using Freeform SQL the linkId columns should be part of the select statement. LinkId columns should be unique identifiers.  |
| **BEHAVIOR** | NO | This class of data change is when a a section of your data is drifting from its normal tendency there is no 1 record to link. |
| **SCHEMA** | NO | This class of data change is at a schema/dataset level there are no records to link. |
| **RECORD** | PARTIAL | In some cases when a record is added or removed it may be available for linking. |
| **PATTERN** | NO | Patterns are not always a direct link.  This item is still under performance review. |

### Notebook API Example

```text
+------------+----------+-------+-------+-----+-----------------+---------------+
|     dataset|     runId|fieldNm| format|count|          percent| transaction_id|
+------------+----------+-------+-------+-----+-----------------+---------------+
|      order |2018-02-24|  fname|xxxx'x.|    1|7.142857142857142|t-1232         |
+------------+----------+-------+-------+-----+-----------------+---------------+
```

```scala
owl.getShapesDF 
```

### Rest API Example

When supplying a linkId Owl will naturally exclude this field from most activities.  Meaning a unique ID or primary key column can not be duplicative or it would not be the primary key, hence it will not be evaluated for duplicates.  The same goes for Outliers and Shapes as a large sequence number or other variations might trigger a false positive when this column is denoted to be simply for the purpose of linking uniquely back to the source.  If you for some reason want to also evaluate this column as well as link it please create a derived column with a different name and Owl will naturally handle both cases.    

```scala
owl.getShapes
owl.getDupes
owl.getOutliers
owl.getRuleBreaks
owl.getSourceBreaks
```

### getRules\(\)

```scala
----Rules----
+-----------------+----------+--------------------+------------------+------+
|          dataset|     runId|              ruleNm|         ruleValue|linkId|
+-----------------+----------+--------------------+------------------+------+
|dataset_outlier_3|2018-02-24|     fname_like_Kirk|fname like 'Kirk' |  c-41|
|dataset_outlier_3|2018-02-24|     fname_like_Kirk|fname like 'Kirk' |  c-42|
|dataset_outlier_3|2018-02-24|     fname_like_Kirk|fname like 'Kirk' |  c-43|
|dataset_outlier_3|2018-02-24|     fname_like_Kirk|fname like 'Kirk' |  c-44|
|dataset_outlier_3|2018-02-24|     fname_like_Kirk|fname like 'Kirk' |  c-45|
|dataset_outlier_3|2018-02-24|if_email_is_valid...|             email|  c-31|
|dataset_outlier_3|2018-02-24|if_email_is_valid...|             email|  c-33|
|dataset_outlier_3|2018-02-24|if_zip_is_valid_Z...|               zip|  c-40|
+-----------------+----------+--------------------+------------------+------+
```

### getDupes\(\)

first split on ~~ then if you have a multiple part key split on ~\|

```scala
----Dupes----
+-----------------+----------+-----+--------------------+----------+
|          dataset|     runId|score|                 key|    linkId|
+-----------------+----------+-----+--------------------+----------+
|dataset_outlier_3|2018-02-24|  100|9ec828d5194fa397b...|c-45~~c-36|
|dataset_outlier_3|2018-02-24|  100|1f96274d1d10c9f77...|c-45~~c-35|
|dataset_outlier_3|2018-02-24|  100|051532044be286f99...|c-45~~c-44|
|dataset_outlier_3|2018-02-24|  100|af2e96921ae53674a...|c-45~~c-43|
|dataset_outlier_3|2018-02-24|  100|ad6f04bf98b38117a...|c-45~~c-42|
|dataset_outlier_3|2018-02-24|  100|1ff7d50a7a9d07d02...|c-45~~c-41|
|dataset_outlier_3|2018-02-24|  100|6ed858ed1f4178bb0...|c-45~~c-40|
|dataset_outlier_3|2018-02-24|  100|d2903703b348fb4cb...|c-45~~c-39|
|dataset_outlier_3|2018-02-24|  100|24bf54412de1e720d...|c-45~~c-38|
|dataset_outlier_3|2018-02-24|  100|7a7ce0beb41b39564...|c-45~~c-37|
+-----------------+----------+-----+--------------------+----------+
```

