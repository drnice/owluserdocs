# Performance Tests

## Load and Profile

| Dataset | GBs | Rows | Cols | Execs | Cores | Memory | Runtime |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| NYSE | 0.1G | 102,000 | 8 | 1 | 1 | 1G | 00:00:48 |
| AUM | 14G | 9,000,000 | 48 | 6 | 1 | 4G | 00:07:13 |
| ENERGY |  | 43,000,000 | 6 | 8 | 3 | 3G | 00:04:35 |

### NYSE

```bash
-bhtimeoff -numexecutors 1 
-lib "/opt/owl/drivers/postgres" 
-executormemory 1g 
-h metastore01.us-east1-b.c.owl-hadoop-cdh.internal:5432/dev?currentSchema=public 
-drivermemory 1g -master k8s:// -ds public.nyse_128 -deploymode cluster 
-q "select * from public.nyse" -bhlb 10 -rd "2020-10-26" 
-driver "org.postgresql.Driver" -bhminoff 
-loglevel INFO -cxn postgres-gcp -bhmaxoff
```

### AUM

```bash
-owluser kirk 
-lib "/opt/owl/drivers/postgres" -datashapeoff 
-numpartitions 6 -ds public.aum_dt2_50 
-deploymode cluster -bhlb 10 -bhminoff 
-cxn postgres-gcp -bhmaxoff -bhtimeoff 
-numexecutors 6 
-executormemory 4g -semanticoff 
-h metastore01.us-east1-b.c.owl-hadoop-cdh.internal:5432/dev?currentSchema=public 
-columnname aum_id -corroff -drivermemory 4g -master k8s:// 
-q "select * from public.aum_dt2" -histoff -rd "2020-10-27" 
-driver "org.postgresql.Driver" -loglevel INFO -agentjobid 7664
```

### ENERGY

```bash
-f "hdfs:///demo/owl_usage_all.csv" \
-rd "2019-02-02" \
-ds energy_file \
-loglevel DEBUG -readonly \
-d "," -df dd-MMM-yy \
-master yarn \
-deploymode client  \
-numexecutors 3 \
-executormemory 10g
```

