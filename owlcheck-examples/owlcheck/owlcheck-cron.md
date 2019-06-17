---
description: Template for Job Control
---

# OwlCheck Cron

### Cron / Autosys / Control M / Oozie

It is common for organization to need to run jobs on a schedule.  Below are a few shell tricks to get a date from bash and use an OwlCheck with template variables.

Kinit and get run\_date from shell or job control variable, pass it into Owl using $run\_date

```bash
%sh
run_date=$(date +%Y-%m-%d)
run_date=$(date '+%Y-%m-%d %H:%M')
echo $run_date

#kinit
echo "password" | kinit  userabc@CW.COM

~/owl/bin/owlcheck -q "select * from lake.stock_eod where date = '2017-01-26' " \
-u user -p pass \
-c "jdbc:mysql://owldatalake.chzid9w0hpyi.us-east-1.rds.amazonaws.com:3306" \
-rd $run_date \
-dc "date" \
-dl \
-dllb 7 \
-dlminhist 2 \
-tbin DAY \
-dlkey sym,exch \
-ds "lake.stock_nasdaq" \
-driver "com.mysql.jdbc.Driver" \
-lib "/home/ec2-user/owl/drivers/mysql/" \
-master yarn -deploymode client -numexecutors 1 -executormemory 1g \
-loglevel DEBUG
```

