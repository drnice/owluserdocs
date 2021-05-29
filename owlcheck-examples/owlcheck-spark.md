# OwlCheck Spark

### Scale + Data Science

Where Scale meets Data Science.  Scale linearly with your data by adding executors and/or memory

```text
-f "file:///Users/home/salary_data.csv" \
-d "," \
-rd "2018-01-08" \
-ds "salary_data"
-numexecutors 2 \
-executormemory 2g
```

### Yarn Master

If Owl is run on an edge node on a popular hadoop distribution such as HDP, CDH, EMR it will automatically register the jobs with Yarn Resource Manager.

### Spark Master

Owl can also run using spark master by using the -master input and passing in spark:url

### Spark Standalone

Owl can run in standalone most but naturally will not distribute the processing beyond the hardware it was activated on.

| Options | Description |
| :--- | :--- |
| deploymode | spark deploymode option |
| drivermemory | driver memory example 3G for local space |
| executorcores | spark executor cores |
| executormemory | spark executor memory option example 3G |
| master | overrides local\[\*\], i.e. spark://myhost:7077, yarn-client, yarn-cluster |
| sparkprinc | kerberos principal name ex: owl@OWL.COM |

### Use Spark-Submit directly bypassing OwlCheck

```bash
spark-submit \
--driver-class-path /opt/owl/drivers/postgres42/postgresql-42.2.4.jar \
--driver-library-path /opt/owl/drivers/postgres42/postgresql-42.2.4.jar \
--driver-memory 3g --num-executors 2 --executor-memory 1g \
--master spark://Kirks-MBP.home:7077 \
--class com.owl.core.cli.OwlCheck /opt/owl/bin/owl-core-trunk-jar-with-dependencies.jar \
-u user -p pass -c jdbc:postgresql://owlpostgres.chzid9w0hpyi.us-east-1.rds.amazonaws.com/postgres \
-ds accounts -rd 2019-05-05 -dssafeoff -q "select * from accounts"
-driver org.postgresql.Driver -lib /opt/owl/drivers/postgres42/  
```

### Parallel JDBC Spark-Submit

```bash
spark-submit \
--driver-class-path /opt/owl/drivers/postgres42/postgresql-42.2.4.jar \
--driver-library-path /opt/owl/drivers/postgres42/postgresql-42.2.4.jar \
--conf spark.driver.extraJavaOptions=-Dlog4j.configuration=file:///opt/owl/config/log4j-TRACE.properties \
--conf spark.executor.extraJavaOptions=-Dlog4j.configuration=file:///opt/owl/config/log4j-TRACE.properties \
--files /opt/owl/config/log4j-TRACE.properties \
--driver-memory 2g --num-executors 2 --executor-memory 1g --master spark://Kirks-MBP.home:7077  \
--class com.owl.core.cli.OwlCheck /opt/owl/bin/owl-core-trunk-jar-with-dependencies.jar \
-u us -p pass -c jdbc:postgresql://owlpostgres.chzid9w0hpyi.us-east-1.rds.amazonaws.com/postgres \
-ds aumdt -rd 2019-05-05 -dssafeoff -q "select * from aum_dt" \
-driver org.postgresql.Driver -lib /opt/owl/drivers/postgres42/  \
-connectionprops fetchsize=6000 -master spark://Kirks-MBP.home:7077 \
-corroff -histoff -statsoff \
-columnname updt_ts -numpartitions 4 -lowerbound 1557597987353 -upperbound 1557597999947
```

