# Position Limit Intraday



### Ingesting Intraday Files

Here we illustrate an example of how to work with files when using Owl programmatically. This can be implemented in both a Notebook setting and in your own codebase.

```scala
  ///////////////////////////////////////////////////////////////////////////
    //                  USE CASE - Ingesting Intraday Files                  //
    ///////////////////////////////////////////////////////////////////////////

    // Part of your pipeline includes the ingestion of files that have the date
    // and hour encoded in the file name. How do you process those files using Owl?
    //
    // Format: <name>_<year>_<month>_<day>.csv
    //
    // Build up a data structure containg the files you want to process (here we
    // just use a simple list, but you may want to be pulling from a pubsub
    // queue, AWS bucket, etc...). Here we just use a simple file list of 6
    // hours of trade position data.
    val position_files = List(
      new File(getClass.getResource("/position_file_2019_11_03_08.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_09.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_10.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_11.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_12.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_13.csv").getPath),
      new File(getClass.getResource("/position_file_2019_11_03_14.csv").getPath))

    // Create your spark session.
    val spark = SparkSession.builder
      .master("local")
      .appName("test")
      .getOrCreate()

    // Configure Owl.
    val opt = new OwlOptions
    opt.dataset = "positions"
    opt.load.delimiter = ","
    opt.spark.master = "local[1]"
    opt.outlier.on = true
    opt.outlier.key = Array("cid")
    opt.outlier.timeBin = TimeBin.HOUR
    // Customize this to only process a subset of the data.
    opt.load.fileQuery = "select * from dataset"

    position_files.foreach { file: File =>
      // Tell Owl where to find the file.
      opt.load.filePath = file.getPath

      // Parse the filename to construct the run date (-rd) that will be passed
      // to Owl.
      val name = file.getName.split('.').head
      val parts = name.split("_")
      val date = parts.slice(2, 5).mkString("-")
      val hour = parts.takeRight(1).head

      // Must be in format 'yyyy-MM-dd' or 'yyyy-MM-dd HH:mm'.
      val rd = s"${date} ${hour}"

      // Tell Owl to process data
      opt.runId = rd

      // Create a DataFrame from the file.
      val df = OwlUtils.load(opt.load.filePath, opt.load.delimiter, spark)

      // Instantiate an OwlContext with the dataframe and our custom configuration.
      val owl = OwlUtils.OwlContext(df, spark, opt)

      // Make sure Owl has catalogued the dataset.
      owl.register(opt)

      // Let Owl do the rest!
      owl.owlCheck()

    }
```

