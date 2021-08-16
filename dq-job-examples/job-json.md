# DQ Job JSON

## Files

Run against a file using -json.  Additionally, options are available for -flatten and -multiline.  This is helpful for nested and various formats.

```
-ds json_file_example \
-f s3a://bucket_name/file.json \
-h sandbox-owl.us-east4-c.c.owl-node.internal:5432/postgres \
-master spark://sandbox-owl.us-east4-c.c.owl-node.internal:7077 \
-json \
-flatten \
-multiline 
```

{% hint style="info" %}
Automatic flattening will infer schema and explode all structs, arrays, and map types.
{% endhint %}

## Using Spark SQL 

```bash
-ds public.json_sample \ 
-lib "/opt/owl/drivers/postgres/" \
-h sandbox-owl.us-east4-c.c.owl-node.internal:5432/postgres \
-master spark://sandbox-owl.us-east4-c.c.owl-node.internal:7077 
-q "select * from public.jason" 
-rd "2021-01-17" 
-driver "org.postgresql.Driver" 
-cxn postgres-gcp 
-fq "select  \
get_json_object(col_3, '$.data._customer_name') AS  `data_customer_name` , \
get_json_object(col_3, '$.data._active_customer') AS  `data_active_customer` , \
from dataset "  

```

{% hint style="info" %}
Pass in the path to Owls' -fq parameter.  This is great for mixed data types within a database.  For example, if you store JSON data as a string or a blob among other data.
{% endhint %}

```bash
// Flatten
val colArr = new JsonReader().flattenSchema(df.schema)
colArr.foreach(x => println(x))
```

{% hint style="success" %}
This Owl utility will traverse the entire schema and print the proper get JSON object spark sql strings.  You can use this instead of typing each query statement into the command line -fq parameter as seen above. 
{% endhint %}

## Using Owl Libraries

{% code title="" %}
```bash
import com.owl.common.options._
import com.owl.core.util.OwlUtils
import com.owl.core.activity2.JsonReader

val connProps = Map (
  "driver"   -> "org.postgresql.Driver",
  "user"     -> "user",
  "password" -> "password",
  "url"      -> "jdbc:postgresql://10.173.0.14:5432/postgres",
  "dbtable"  -> "public.data"
)

// Spark 
var rdd = spark.read.format("jdbc").options(connProps).load.select($"col_name").map(x=>x.toString()).rdd
var df = spark.read.json(rdd)

// Flatten
val colArr = new JsonReader().flattenSchema(df.schema)
val flatJson = df.select(colArr: _*)
flatJson.cache.count

// Opts
val dataset = "json_example"
val runId = s"2021-01-14"
val opt = new OwlOptions()
opt.dataset = dataset
opt.runId = runId
opt.datasetSafeOff = true

// Owlcheck
OwlUtils.resetDataSource("sandbox-owl.us-east4-c.c.owl-node.internal","5432/postgres","danielrice","owl123", spark)
val owl = OwlUtils.OwlContext(flatJson, opt)
owl.register(opt)
owl.owlCheck
```
{% endcode %}

{% hint style="info" %}
### JsonReader\(\)

This uses Owl's JsonReader to do the heavy lifting. 
{% endhint %}



