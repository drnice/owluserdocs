# OwlCheck Files

### **Outliers on a single large file**  <a id="HOutliersonasinglelargefile"></a>

If data is in one single file \(spanning multiple time periods\), you can apply the -fullfile option for outlier detection. This will load the entire file so you can do lookbacks across multiple dates.

```bash
./owlcheck -ds energy_fullfile_usage_outliers -rd "2017-11-30" \
-f hdfs:///user/userspark/owl_usage_all.csv -d , \
-filter "NOV-17" \
-transform "READ_END=to_date(CAST(READ_END AS STRING), 'dd-MMM-yy') as READ_END" \
-fq "select MWH, ANON_ACCT_ID, READ_END from dataset where READ_END > '2017-11-01' and READ_END < '2017-11-30  " \
-fullfile \
-dl -tbin MONTH -by MONTH -dllb 12 -dlkey ANON_ACCT_ID -dc READ_END \
-corroff -histoff -statsoff \
-master yarn -deploymode client \
-drivermemory 3g -numexecutors 3 -executormemory 2g  -h cdh-edge.us-east1-b.c.owl-hadoop-cdh.internal:2181 \
```

### **Outliers on a series of smaller files**  <a id="HOutliersonaseriesofsmallerfiles"></a>

If data is loaded in smaller files that only contain a single date period, you can apply the -fllb file lookback option. This will aggregate previous run files into a single dataset so you can lookback across multiple dates.

```bash
./owlcheck -f /Users/brian/Downloads/csv2/20190102*.csv \
-ds outlier_smaller_files -rd 2019-01-02 \
-filternot F1233 -filter "20190102" \
-nulls "N.A." -zfn -transform "PX_HIGH=CAST(PX_HIGH as double)" -fllb \
-dc OWL_RUN_ID -adddc \
-dl -dlkey B_SECURITY_ID -dllb 5 -tbin DAY -by DAY -catoff \
-loglevel TRACE -dlminhist 1 \
```

```bash
./owlcheck -f /Users/brian/Downloads/csv2/20190103*.csv \
-ds outlier_smaller_files -rd 2019-01-03 \
-filternot F1233 -filter "20190103" \
-nulls "N.A." -zfn -transform "PX_HIGH=CAST(PX_HIGH as double)" -fllb \
-dc OWL_RUN_ID -adddc \
-dl -dlkey B_SECURITY_ID -dllb 5 -tbin DAY -by DAY -catoff \
-loglevel TRACE -dlminhist 1 
```

