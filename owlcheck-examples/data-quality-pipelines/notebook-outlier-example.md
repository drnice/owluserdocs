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

val df = OwlUtils.load(filePath = filePath, delim = ",", sparkSession = spark)

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

val dfCurrent = df.where(s"app_date = '${opt.runId}' ")
val owl = OwlUtils.OwlContextWithHistory(dfCurrent = dfCurrent, dfHist = df, opt = opt)
owl.register(opt)
owl.owlCheck()
```

### Owl Web UI

Score drops from 100 to 99 based on the single outlier in the file. Row count is 1 because there is only 1 row in the current data frame.  The historical data frame was provided for context and you can see those rows in the outlier drill-in.  The customer\_id is available in the data preview and can be used as an API hook to link back to the original dataset.  

![](../../.gitbook/assets/owl-df-with-hist-customer_id.png)

