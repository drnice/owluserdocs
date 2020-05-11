# Simple Spark Data Pipeline

## Load Table use SparkJDBC

```scala
//--- Configure Table From Database ---// 
val connProps = Map (
  "driver"   -> "org.postgresql.Driver",
  "user"     -> s"${user}",
  "password" -> s"${pass}",
  "url"      -> s"jdbc:postgresql://${host}:${port}/${database}",
  "dbtable"  -> "owl_test.nyse"
)

//--- Load Spark DataFrame ---//
val jdbcDF = spark.read.format("jdbc").options(connProps).load
jdbcDF.show
```

## Configure Owl Options

Connect to Owl's Metadata Database and control DQ scan options.  Wrap sparkDF with Owl context.

```scala
import com.owl.common.options._
import com.owl.core.util.OwlUtils

val opt = new OwlOptions
//--- Owl Metastore ---//
opt.host = s"$owlHost"
opt.port = s"5432/postgres?currentSchema=public"
opt.pgUser = s"$owlUser"
opt.pgPassword = s"$owlPass"
//--- Run Options ---//
opt.dataset = "owl_test.nyse"
opt.runId = "2018-01-10"
opt.datasetSafeOff = true

val owl = OwlUtils.OwlContext(jdbcDF, opt)
```

## Register with Catalog and Run Profile

```scala
//--- Register with Owl Catalog ---//
owl.register(opt)

//--- Profile Dataset ---//
val profile = owl.profileDF
profile.show
```

Notice that Owl returns results as Dataframes.  This is a fantastic abstraction that allows you to ignore all domain objects and custom types and interact with a scaleable generic result set using common protocols like "where" or "filter" or "save" or "write" all with parallel operations. 

```scala
+--------------+-----+-------+-----------+---+---+--------+-----------+------+----+------+-------+-------+------+----+---------+
|        column|nulls|empties|cardinality|min|max|is_mixed|mixed_ratio|   Int|Long|String|Decimal|Boolean|Double|Date|Timestamp|
+--------------+-----+-------+-----------+---+---+--------+-----------+------+----+------+-------+-------+------+----+---------+
|     tenant_id|    0|      0|         60|  0|  9|   false|        0.0|100000|   0|     0|      0|      0|     0|   0|        0|
|           a11|    0|      0|          1|a11|a11|   false|        0.0|     0|   0|100000|      0|      0|     0|   0|        0|
|           a10|    0|      0|          1|a10|a10|   false|        0.0|     0|   0|100000|      0|      0|     0|   0|        0|
|  account_type|    0|      0|          3| 02| 06|   false|        0.0|100000|   0|     0|      0|      0|     0|   0|        0|
|           a13|    0|      0|          1|a13|a13|   false|        0.0|     0|   0|100000|      0|      0|     0|   0|        0|
|security_alias|    0|      0|          3|  0|  2|   false|        0.0|100000|   0|     0|      0|      0|     0|   0|        0|
|           a12|    0|      0|          1|a12|a12|   false|        0.0|     0|   0|100000|      0|      0|     0|   0|        0|
+--------------+-----+-------+-----------+---+---+--------+-----------+------+----+------+-------+-------+------+----+---------+
```

### Profile UI

While the spark DF.show\(\) is a nice and convenient output format, you may prefer a rich UI visual that tracks the data tests over time.  The UI provides trend analysis, data drift, data relationships and more.

![](../../.gitbook/assets/owl-profiler.png)

## Duplicates

Take duplicate detection for example.  A common use-case where a business wants to make sure they do not have repeated or duplicate records in a table.  Set the lowerBound to the percent fuzzy match you are willing to accept, commonly 87% or higher is an interesting match.  You might also want to target a single day or week or month that you shouldn't have dupes within.  Notice the .where function and then pass in a custom dataframe to the Owl context.

```scala
opt.dupe.on = true
opt.dupe.lowerBound = 99
opt.dupe.include = Array("SYMBOL", "EXCH")

val df1Day = jdbcDF.where("TRADE_DATE = '2018-01-10' ")
val owl = OwlUtils.OwlContext(df1Day, opt)

val dupes = owl.dupesDF
dupes.show

// rdd collect
dupes.rdd.collect.foreach(println)

// records linked together for remediation
owl.getDupeRecords.show
```

## Outliers

Gaining and understanding of your outliers is a commonly desired DQ function.  Owl has several configurations to help find the most meaningful outliers in your dataset and over time.   Below compares the current day to a baseline of days in the historical dataframe.

```scala
opt.outlier.on = true
opt.outlier.lookback = 6
opt.outlier.dateColumn = "TRADE_DATE"
opt.outlier.timeBin = OutlierOpt.TimeBin.DAY
opt.outlier.key = Array("SYMBOL")

val df1Day = jdbcDF2.where("TRADE_DATE = '2018-01-10' ")
val owl = OwlUtils.OwlContextWithHistory(dfCurrent = df1Day, dfHist = jdbcDF2, opt = opt)
val outliers = owl.outliersDF
outliers.show
```

