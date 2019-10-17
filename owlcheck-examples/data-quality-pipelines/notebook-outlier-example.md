# Notebook Outlier Example

This real life use-case is when you have a large file or data frame with many days of data but you want the run profile to be the current day so that it trends properly overtime.  Another nuance to this use-case is that the customer\_id is a unique field to the user and it should not show up in the analytics i.e. an outlier.  But the customer\_id should be available when the user wants to query the rest api end points.  The customer\_id is then used to link back the users original dataset.  A bloomberg\_Id \(BB\_ID\) is a common example.

### CSV File

```text
fname,app_date,age,customer_id
Kirk,2018-02-24,18,31
Kirk,2018-02-23,11,4
Kirk,2018-02-22,10,3
Kirk,2018-02-21,12,2
Kirk,2018-02-20,10,1
```

### Notebook Code \(Spark Scala\)

```scala
val filePath = getClass.getResource("/notebooktest.csv").getPath

val spark = SparkSession.builder
  .master("local")
  .appName("test")
  .getOrCreate()

val opt = new OwlOptions()
opt.runId = "2018-02-24"
opt.dataset = "dataset_outlier"
opt.load.datasetSafety = false
opt.outlier.on = true
opt.outlier.lookback = 5
opt.outlier.key = Array("fname")
opt.outlier.timeBin = OutlierOpt.TimeBin.DAY
opt.outlier.dateColumn = "app_date"
opt.outlier.excludes = Array("customer_id")

val dfHist = OwlUtils.load(filePath = filePath, delim = ",", sparkSession = spark)
val dfCurrent = dfHist.where(s"app_date = '${opt.runId}' ")

val owl = OwlUtils.OwlContextWithHistory(dfCurrent=dfCurrent, dfHist=dfHist, opt=opt)
owl.register(opt)
owl.owlCheck()
```

### Owl Web UI

Score drops from 100 to 99 based on the single outlier in the file. Row count is 1 because there is only 1 row in the current data frame.  The historical data frame was provided for context and you can see those rows in the outlier drill-in.  The customer\_id is available in the data preview and can be used as an API hook to link back to the original dataset.  

![](../../.gitbook/assets/owl-df-with-hist-customer_id.png)



1. Request URL:http://localhost:9000/v2/getoutlier?dataset=dataset\_outlier&runId=2018-02-24T05:00:00.000+0000
2. Request Method:GET

```markup
http://$host:9000/v2/getoutlier?dataset=dataset_outlier&runId=2018-02-24T05:00:00.000+0000
```

{% api-method method="get" host="" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```bash
{
  confidence: 77
  dataset: "dataset_outlier"
  keyArr: null
  lb: 0
  outColumn: "age"
  outKey: "Kirk"
  outMedian: "10.5"
  outValue: "18.0"
  runId: "2018-02-24T05:00:00.000+0000"
  ub: 0
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

```bash
{
  confidence: 77
  dataset: "dataset_outlier"
  keyArr: null
  lb: 0
  outColumn: "age"
  outKey: "Kirk"
  outMedian: "10.5"
  outValue: "18.0"
  runId: "2018-02-24T05:00:00.000+0000"
  ub: 0
}
```

