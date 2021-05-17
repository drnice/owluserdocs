# More...

An OwlCheck is bash script that is essentially the launch point for any owl job to scan a dataset. A dataset can be a flat file \(such as textfile, json file, parquet file, etc\), or a table from any number of Databases \(such as Oracle, Postgres, Mysql, Greenplum, DB2, SQLServer, Teradata, etc\).

Example Run a Data Quality check on any file by setting the file path.

```bash
./owlcheck -ds stock_trades -rd 2019-02-23 -f /path/to/file.csv -d ,
```

Example output below. A hoot is a valid JSON response

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

## Monthly Data

Sometimes you may want to run monthly profiles with aggregated data. In this case the scheduling tool can supply the ${rd} as variable such as $runDate and the end date as $endDate. 1 line examples for bash or shell below.

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

## Monthly BackRun \(Using Owl's built in Monthly\)

Owl has 2 convenient features here: 1\) the use of built in ${rd} and ${rdEnd} removes the need for any shell scripting. 2\) using -br, Owl will replay 20 months of data using this template automatically.

```bash
./owlcheck \
-q "select * from table where date >= '${rd}' and date < '${rdEnd}' " \
-ds example
-rd 2019-01-01
-rdEnd 2019-02-01
-tbin MONTH
-br 20
```

## Daily Data

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

## Daily Data \(Using Owl's built in Daily\)

```bash
./owlcheck \
-q "select * from table where date = '${rd}' " \
-ds example \
-rd 2019-03-14
```

## Daily Data with Timestamp instead of Date

```bash
./owlcheck \
-q "select * from table where TS >= '${rd} 00:00:00' and TS <= '${rd} 23:59:59' " \
-ds example \
-rd 2019-03-14
```

## OR Timestamp using ${rdEnd}

```bash
./owlcheck \
-q "select * from table where TS >= '${rd} 00:00:00' and TS < '${rdEnd} 00:00:00' " \
-ds example \
-rd 2019-03-14 \
-rdEnd 2019-03-15 \
-tbin DAY
```

## Hourly Data

```bash
./owlcheck \
-q "select * from table where TS >= '${rd}' and TS < '${rdEnd}' " \
-ds example \
-rd    "2019-03-14 09:00:00" \
-rdEnd "2019-03-14 10:00:00" \
-tbin HOUR
```

## OwlCheck Template with Service Hook

The best practice is to make a generic job that would be repeatable for every OwlCheck. Below is an example that first hits Owl using a REST call and then runs the response.

```bash
curl -X GET "http://$host/v2/getowlchecktemplate?dataset=lake.loan_customer" \
-H "accept: application/json"
```

The above REST call returns the below OwlCheck. It is left up to the Job Control to replace the ${rd} with the date from the Job Control system. You can use Owls built in scheduler to save these steps.

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
-owluser {user}
```

## REST API End Point

The easiest option is to use the **runtemplate** end point API call to make requests to from cmdLine or JobControl System.  This endpoint gets the OwlCheck saved in Owl instead of the client needing to know the OwlCheck details.

{% api-method method="post" host="http://$host" path="/v2/runtemplate?dataset=lake.spotify" %}
{% api-method-summary %}
RunTemplate
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="dataset" type="string" required=true %}
name of dataset.    -ds OR opt.dataset
{% endapi-method-parameter %}

{% api-method-parameter name="rd" type="string" required=false %}
yyyy-MM-dd format can add time or timezone.  if note passed in it will use the current day
{% endapi-method-parameter %}

{% api-method-parameter name="rdEnd" type="string" required=false %}
yyyy-MM-dd format can add time or timezone.  if not passed it will not be used
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "msg": "Success, Owl Check is Running as process 13996",
  "pid": "13996",
  "runid": "2017-01-01",
  "starttime": "Thu Oct 17 13:27:01 EDT 2019",
  "cmd": "cmd": "-ds lake.spotify -rd 2019-10-17   -q \"select * from lake.spotify\" -cxn mysql -lib /opt/owl/drivers/mysql/ -drivermemory 2G -histoff   -owluser {user}",
  "dataset": "lake.spotify"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Curl example for the above Rest Call

```bash
TOKEN=$(curl -s -X POST http://$host/auth/signin -H "Content-Type:application/json" -d "{\"username\":\"$username\", \"password\":\"$password\"}" | jq -r '.token')

curl -i -H 'Accept: application/json' \
  -H "Authorization: Bearer ${TOKEN}" \
  http://$host/v2/runtemplate?dataset=lake.spotify
```

### Bash Script 

A generic and repeatable owlcheck script for job schedulers, that hooks into Owl to get the template.

```bash
#1 authenticate
curl -sb -X POST -d username={user} -d password={password} http://$OWL_HOST/login -c cookies.txt

#2 get template
owlcheck_args=$(curl -b cookies.txt -H "accept: application/json" -X GET http://$OWL_HOST/v2/getowlcheckcmdlinebydataset\?dataset=insurance | sed 's/.*\[\(.*\)\]/\1/' | sed -e "s/^\"//" -e "s/\"$//"  | sed 's/\\\"\(.*\)\\\"/\x27\1\x27/')

#3 replace ${rd} with job_run_date
job_run_date="2019-03-14 10:00:00"
owlcheck_args=${owlcheck_args//'${rd}'/$job_run_date}

#4 run owlcheck
eval owlcheck $owlcheck_args
```

For more Information on Owl's Scheduler check out the doc on **OwlCheck Cron** Page**.**

