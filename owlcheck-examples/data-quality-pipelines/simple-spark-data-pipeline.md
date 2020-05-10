# Simple Spark Data Pipeline

## Load Table use SparkJDBC

```scala
//--- Configure Table From Database ---// 
val connProps = Map (
  "driver"   -> "org.postgresql.Driver",
  "user"     -> s"${user}",
  "password" -> s"${pass}",
  "url"      -> s"jdbc:postgresql://${host}.us-east-1.rds.amazonaws.com:5432/postgres",
  "dbtable"  -> "owl_test.nyse"
)

//--- Load Spark DataFrame ---//
val jdbcDF2 = spark.read.format("jdbc").options(connProps).load
jdbcDF2.printSchema
jdbcDF2.cache
println(jdbcDF2.count)
```

## Configure Owl Options

Connect to Owl's Metadata Database and control DQ scan options.  Wrap sparkDF with Owl context.

```scala
import com.owl.common.options._
import com.owl.core.Owl
import com.owl.core.util.OwlUtils

val opt = new OwlOptions
//--- Owl Metastore ---//
opt.host = s"${owlHost}"
opt.port = s"5432/postgres?currentSchema=public"
opt.pgUser = s"${owlUser}"
opt.pgPassword = s"{owlPass}"
//--- Run Options ---//
opt.dataset = "nyse_notebook_pipeline"
opt.runId = "2018-01-10"
opt.datasetSafeOff = true

val owl = com.owl.core.util.OwlUtils.OwlContext(jdbcDF2, opt)
```

## Register with Catalog and Run Profile

```scala
//--- Register with Owl Catalog ---//
owl.register(opt)

//--- Profile Dataset ---//
val profile = owl.profileDF
profile.show
```

