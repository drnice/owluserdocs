# DQ Job MySql

### Video Tutorial \(MySQL\)

Add automatic data quality to any database in 60 seconds.  This example shows a single table being selected for DQ, however Owl also provides the ability to scan all schemas and tables at once.

{% embed url="https://vimeo.com/372286610" %}



Connect to any database using JDBC.  Mysql example below.  

```bash
-q "select * from lake.stock_eod where date = '2017-01-20' " \
-u username -p password \
-c "jdbc:mysql://owldatalake.chzid9w0hpyi.us-east-1.rds.amazonaws.com:3306" \
-rd "2017-01-20" \
-dc "date" \
-ds "stocks" \
-driver com.mysql.jdbc.Driver \
-lib "/home/ec2-user/owl/drivers/mysql/"
```

