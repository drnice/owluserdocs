# OwlCheck JDBC

Connect to any database via JDBC.

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

![](../../.gitbook/assets/owl-connection.png)

### Fetch Size

It is important to consider the drivers fetch size when loading greater than 1 Million rows across the network.  Owl allows you to set this driver property in the WebApp but this is only for web interaction therefore "fetchsize" will not help here.  Owl also allows fetchsize in the OwlCheck by passing in a connection property.

#### CMD line

```text
-connectionprops "fetchsize=3000"
```

#### Notebook

```text
props.connectionProps.put("fetchsize", "3000")
```

## Parallel JDBC

For greater performance or moving large datasets across a network Owl supports parallel JDBC, which can be enabled by passing `numpartitions` to Owlcheck. This can be a 2-5X improvement in many cases. 

```bash
-lib "/opt/owl/drivers/mysql8/"
-cxn mysql
-q "select * from lake.nyse where trade_date = '${rd}' "
-rd 2018-01-01
-ds nyse
-columnname volume
-numpartitions 4
-lowerbound "0"
-upperbound "5000000000"
-usesql
```

Owl also supports auto parallelization, which will configure the `numPartitions` parameter for you based on the size of your data. This is enabled in the UI when you create a dataset using the Owlcheck wizard.

![](../../.gitbook/assets/screen-shot-2019-10-17-at-4.38.04-pm.png)

