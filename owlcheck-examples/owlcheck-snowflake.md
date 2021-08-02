# OwlCheck Snowflake

## Example CMD Line

```
-h <IP_ADDRESS>:5432/postgres \
-drivermemory 4g \
-master spark://<SPARK_MASTER>:7077 \
-ds PUBLIC.TRANSLATION \
-deploymode client \
-q "select * from PUBLIC.TRANSLATION" \
-rd "2021-07-24" \
-driver "net.snowflake.client.jdbc.SnowflakeDriver" \
-cxn snowflake 
```

### Example JDBC Connection URL

jdbc:snowflake://&lt;IP\_ADDRESS&gt;.snowflakecomputing.com?db=DEMODB&warehouse=COMPUTE\_WH&schema=PUBLIC

### Drive Name

net.snowflake.client.jdbc.SnowflakeDriver



