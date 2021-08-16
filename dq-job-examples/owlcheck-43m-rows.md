# OwlCheck 43M rows

Owl commonly benchmarks on large daily datasets.  In this case a 43 million row table with 12 columns completes in under 6 mins \(5:30\).  The best balance for this dataset was 3 executors each with 10G of ram. 

```text
./owlcheck \
-u user -p password \
-c jdbc:mysql://owldatalake.chzid9w0hpyi.us-east-1.rds.amazonaws.com:3306 \
-q "select * from silo.account_large where acc_upd_ts > '2018-02-01 05:0:00'" \
-rd 2019-02-02 \
-ds account_large \
-dc acc_upd_ts \
-corroff \
-histoff \
-driver com.mysql.cj.jdbc.Driver \
-lib "/home/ec2-user/owl/drivers/mysql/" \
-master yarn \
-deploymode client \
-numexecutors 3 \
-executormemory 10g \
-histoff -corroff -loglevel DEBUG -readonly
```

_note:  not all Owl features were turned on during this run.  On large datasets it is worth it to consider limiting the columns, owl-features, or lookbacks if they are not of interest._

