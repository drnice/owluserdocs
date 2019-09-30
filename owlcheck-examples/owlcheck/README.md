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
-ds example \
-rd $runDate \
-tbin MONTH
```

### Monthly BackRun \(Using Owl's built in Monthly\)

Owl has 2 convenient features here: 1\) the use of built in ${rd} and ${rdEnd} removes the need for any shell scripting.  2\) using -br, Owl will replay 20 months of data using this template automatically.   

```bash
./owlcheck \
-q "select * from table where date >= '${rd}' and date < '${rdEnd}' " \
-ds example
-rd 2019-01-01
-rdEnd 2019-02-01
-tbin MONTH
-br 20
```

### Daily Data

One of the most common examples is data loading or running once a day. A job control framework can pass in this value or you can pull it from shell.

```bash
echo "Hello World Owl"

runDate=$(date +"%Y-%m-%d")
echo $runDate

./owlcheck \
-q "select * from table where date = '$runDate' " \
-ds example \
-rd $runDate \
-tbin DAY
```

### Daily Data \(Using Owl's built in Daily\)

```bash
./owlcheck \
-q "select * from table where date = '${rd}' " \
-ds example \
-rd 2019-03-14
```

### OwlCheck Template with Service Hook

The best practice is to make a generic job that would be repeatable for every OwlCheck.  Below is an example that first hits Owl using a REST call and then runs the response.

```bash
curl -X GET "http://$host/v2/getowlchecktemplate?dataset=lake.loan_customer" \
-H "accept: application/json"
```

The above REST call returns the below OwlCheck.  It is left up to the Job Control to replace the ${rd} with the date from the Job Control system.  You can use Owls built in scheduler to save these steps.

```bash
./owlcheck \
-lib "/home/danielrice/owl/drivers/mysql/" \
-cxn mysql \
-q "select * from lake.loan_customer where load_dt = '${rd}' " \
-key post_cd_num -ds lake.loan_customer \
-rd ${rd} \
-dc load_dt -dl -dlkey usr_name,post_cd_num -dllb 5 \
-tbin DAY -by DAY -dupe -dupeinc ip_address_home,usr_name -dupecutoff 85 \
-fpgon -fpgkey usr_name,post_cd_num -fpgdc load_dt -fpglb 5 -fpgtbin DAY \
-loglevel INFO \
-h $host:5432/owltrunk \
-owluser geoff@owl.com 
```

### Putting it all together

A generic and repeatable owlcheck script for job schedulers, that hooks into Owl to get the template. 

```bash
#1 authenticate
curl -sb -X POST -d username=admin -d password=adminowl http://35.194.67.74/login -c cookies.txt

#2 get template
owlcheck=$(curl -b cookies.txt -H "accept: application/json" -i -X GET  http://35.194.67.74/v2/getowlchecktemplatebydataset?dataset=kirk_nyse_pg)

#3 replace ${rd} with job_run_date
owlcheck = owlcheck.replace('${rd}', $job_run_date)

#4 run owlcheck
exec owlcheck
```

For more Information on Owl's Scheduler check out the doc on **OwlCheck Cron** Page**.**

