# OwlCheck JDBC



Connect to any database via JDBC.

```text
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

