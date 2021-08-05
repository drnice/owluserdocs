# Notebook ColMatch Example

This example shows how one can get column level match statistics across datasources in an Owl Notebook. Supports exact and fuzzy matching.

## Set ColMatch Parameters

```scala
    %spark
    import com.owl.common.domain._
    import com.owl.common.Props
    import com.owl.core.util.OwlUtils
    import scala.collection.JavaConverters._
    import com.owl.common.Utils
    val c1 = new Connection()
    c1.dataset = "silo.account"
    c1.user = "user"
    c1.password = "pass"
    c1.query = "select id, networth, acc_name, acc_branch from silo.account limit 200000"
    c1.url = "jdbc:mysql://<db url>:3306"
    
    val c2 = new Connection()
    c2.dataset = "silo.user_account"
    c2.user = "user"
    c2.password = "pass"
    c2.query = "SELECT acc_name, acc_branch, networth FROM silo.account limit 200000"
    c2.url = "jdbc:mysql://<db url>:3306"
    
    val c3 = new Connection()
    c3.dataset = "silo.user_account"
    c3.user = "user"
    c3.password = "pass"
    c3.query = "SELECT acc_name as acc_name2, acc_branch, networth FROM silo.account limit 100000"
    c3.url = "jdbc:mysql://<db url>:3306"
    
    props.dataset = "colMatchTest1"
    props.runId = "2017-02-04"
    props.connectionList = List(c1,c2,c3).asJava
    props.colMatchBatchSize = 2
    props.colMatchDurationMins = 3
    val owl = OwlUtils.OwlContext(spark.emptyDataFrame, props)
```

### Exact Match

```scala
%spark
props.colMatchLevel = "exact"
owl.register(props)
owl.colMatchDF().show
```

#### Sample Result

```scala
+------------+-----------------+----------+----------+---------------+
|   dataset_1|        dataset_2|     col_1|     col_2|matchPercentage|
+------------+-----------------+----------+----------+---------------+
|silo.account|silo.user_account|        id|  acc_name|              0|
|silo.account|silo.user_account|        id|acc_branch|              0|
|silo.account|silo.user_account|        id|  networth|              0|
|silo.account|silo.user_account|        id|    owl_id|              0|
|silo.account|silo.user_account|  networth|  acc_name|              0|
|silo.account|silo.user_account|  networth|acc_branch|             16|
|silo.account|silo.user_account|  networth|  networth|            100|
|silo.account|silo.user_account|  networth|    owl_id|              0|
|silo.account|silo.user_account|  acc_name|  acc_name|             87|
|silo.account|silo.user_account|  acc_name|acc_branch|              0|
|silo.account|silo.user_account|  acc_name|  networth|              0|
|silo.account|silo.user_account|  acc_name|    owl_id|              0|
|silo.account|silo.user_account|acc_branch|  acc_name|              0|
|silo.account|silo.user_account|acc_branch|acc_branch|             87|
|silo.account|silo.user_account|acc_branch|  networth|             12|
|silo.account|silo.user_account|acc_branch|    owl_id|              0|
|silo.account|silo.user_account|    owl_id|  acc_name|              0|
|silo.account|silo.user_account|    owl_id|acc_branch|              0|
|silo.account|silo.user_account|    owl_id|  networth|              0|
|silo.account|silo.user_account|    owl_id|    owl_id|              0|
+------------+-----------------+----------+----------+---------------+
only showing top 20 rows
```

### Fuzzy Match

```scala
%spark
props.colMatchLevel = "fuzzy"
props.colMatchFuzzyDistance = 4
owl.register(props)
owl.colMatchDF().show
```

#### Sample Result

```scala
+------------+-----------------+----------+----------+---------------+
|   dataset_1|        dataset_2|     col_1|     col_2|matchPercentage|
+------------+-----------------+----------+----------+---------------+
|silo.account|silo.user_account|        id|  acc_name|              5|
|silo.account|silo.user_account|        id|acc_branch|             27|
|silo.account|silo.user_account|        id|  networth|             22|
|silo.account|silo.user_account|        id|    owl_id|              0|
|silo.account|silo.user_account|  networth|  acc_name|            100|
|silo.account|silo.user_account|  networth|acc_branch|            233|
|silo.account|silo.user_account|  networth|  networth|            200|
|silo.account|silo.user_account|  networth|    owl_id|              0|
|silo.account|silo.user_account|  acc_name|  acc_name|            162|
|silo.account|silo.user_account|  acc_name|acc_branch|            262|
|silo.account|silo.user_account|  acc_name|  networth|             75|
|silo.account|silo.user_account|  acc_name|    owl_id|              0|
|silo.account|silo.user_account|acc_branch|  acc_name|            262|
|silo.account|silo.user_account|acc_branch|acc_branch|            612|
|silo.account|silo.user_account|acc_branch|  networth|            175|
|silo.account|silo.user_account|acc_branch|    owl_id|              0|
|silo.account|silo.user_account|    owl_id|  acc_name|              0|
|silo.account|silo.user_account|    owl_id|acc_branch|              0|
|silo.account|silo.user_account|    owl_id|  networth|              0|
|silo.account|silo.user_account|    owl_id|    owl_id|              0|
+------------+-----------------+----------+----------+---------------+
only showing top 20 rows
```

