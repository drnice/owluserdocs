# OwlCheck

An OwlCheck is bash script that is essentially the launch point for any owl job to scan a dataset.  A dataset can be a flat file \(such as textfile, json file, parquet file, etc\), or a table from any number of Databases \(such as Oracle, Postgres, Mysql, Greenplum, DB2, SQLServer, Teradata, etc\).

Example Run a Data Quality check on any file by setting the file path.

```bash
./owlcheck -ds stock_trades -rd 2019-02-23 -f /path/to/file.csv -d ,
```

Example output below.  A hoot is a valid JSON response

```bash
{
  "dataset": "stock_trades",
  "runId": "2019-02-03",
  "score": 100,
  "behaviorScore": 0,
  "rows": 477261,
  "passFail": 1,
  "peak": 1,
  "dayOfWeek": "Sun",
  "avgRows": 0,
  "cols": 5,
  "activeRules": 0,
  "activeAlerts": 0,
  "runTime": "00:00:23",
  "dqItems": {},
  "datashapes": [],
  "validateSrc": [],
  "alerts": [],
  "prettyPrint": true
}
```

### Monthly Data

Sometimes you may want to run monthly profiles with aggregated data.  In this case the scheduling tool can supply the ${rd} as variable such as $runDate and the end date as $endDate.  1 line examples for bash or shell below.

```bash
echo "Hello World Owl"

runDate=$(date +"%Y-%m-%d")
endDate=$(date -d "$runDate +1 month" +%Y-%m-%d)

echo $runDate
echo $endDate

./owlcheck \
-q "select * from table where date >= '$runDate' and date < '$endDate' " \
-ds example
-rd $runDate
-tbin MONTH
```

### Daily Data

One of the most common examples is data loading or running once a day. A job control framework can pass in this value or you can pull it from shell.

```bash
echo "Hello World Owl"

runDate=$(date +"%Y-%m-%d")
echo $runDate

./owlcheck \
-q "select * from table where date = '$runDate' " \
-ds example
-rd $runDate
-tbin DAY
```

