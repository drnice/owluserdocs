# Azure DataBricks - DQ Pipeline

### Run a DQ check on any file in Azure Blob

Read the File by setting up the azure key.

```scala
spark.conf.set("fs.azure.account.key.abcCompany.blob.core.windows.net","GBB6Upzj4AxQld7cFv7wBYNoJzIp/WEv/5NslqszY3nAAlsalBNQ==")

val df = spark.read.parquet("wasbs://company-abc@abceCompany.blob.core.windows.net/FILE_NAME/20190201_FILE_NAME.parquet")

```

Process the file using Owl

```scala
// register in Owl Catalog, Optional
val owl = new Owl(df).register

// run a full DQ Check
owl.owlCheck()
```

Additional imports and input options

```scala
import com.owl.core._
import com.owl.common._

val props = new Props()
props.dataset = datasetName
props.runId = 2019-03-02
props..... // look at the many input options
```

{% embed url="https://owl-analytics.com/Create-a-Data-Quality-Pipeline-using-Owl.html" %}



