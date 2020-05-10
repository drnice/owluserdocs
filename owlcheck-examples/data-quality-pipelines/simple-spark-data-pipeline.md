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

## Duplicates

Take duplicate detection for example.  A common use-case where a business wants to make sure they do not have repeated or duplicate records in a table.  Set the lowerBound to the percent fuzzy match you are willing to accept, commonly 87% or higher is an interesting match.  You might also want to target a single day or week or month that you shouldn't have dupes within.  Notice the .where function and then pass in a custom dataframe to the Owl context.

```scala
opt.dupe.on = true
opt.dupe.lowerBound = 99
opt.dupe.include = Array("SYMBOL", "EXCH")

val df1Day = jdbcDF.where("TRADE_DATE = '2018-01-10' ")
val owl = OwlUtils.OwlContext(df1Day, opt)

val dupes = owl.dupesDF

// dataframe show
dupes.show

// rdd collect
dupes.rdd.collect.foreach(println)

// records linked together for remediation
owl.getDupeRecords.show
```

