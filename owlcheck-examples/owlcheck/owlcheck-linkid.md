# OwlCheck LinkId

Ability to link an OwlCheck findings back to the source record by supplying the primary key in the linkId field.  There are 2 ways to provide the linkId, 1\) a the cmdline via -linkid or 2\) in a notebook via opt.linkId.  Owl supports one or many primary key columns in your datasets for record linkage to your original table, file or dataframe.  If your primary key column contains many columns use a comma to delineate.  Set to released on Nov 15th 2019

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
| **OUTLIER** | YES | Each outlier will have a link back to the detected record for remediation.  If you apply a limit you will only get the limited amount. |
| **DUPE** | YES | Each duplicate or fuzzy match will have a link back to the record for remediation. |
| **SOURCE** | PARTIAL | Each source record that has a cell value that doesn't match to the target will have a link for remediation.  SOURCE will not have links for row counts and schema as these are not record level findings. |
| **RULE** | YES | A handful of record examples that did not meet the condition of the RULE will be provided with links. |
| **BEHAVIOR** | NO | This class of data change is when a a section of your data is drifting from its normal tendency there is no 1 record to link. |
| **SCHEMA** | NO | This class of data change is at a schema/dataset level there are no records to link. |
| **RECORD** | PARTIAL | In some cases when a record is added or removed it may be available for linking. |
| **PATTERN** | PARTIAL | Patterns are not always a direct link.  This item is still under performance review. |

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

coming Nov 10th

When supplying a linkId Owl will naturally exclude this field from most activities.  Meaning a unique ID or primary key column can not be duplicative or it would not be the primary key, hence it will not be evaluated for duplicates.  The same goes for Outliers and Shapes as a large sequence number or other variations might trigger a false positive when this column is denoted to be simply for the purpose of linking uniquely back to the source.  If you for some reason want to also evaluate this column as well as link it please create a derived column with a different name and Owl will naturally handle both cases.    

