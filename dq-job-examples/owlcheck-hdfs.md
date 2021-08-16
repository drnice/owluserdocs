# OwlCheck HDFS



Run Data Quality on a file in HDFS.  Owl will automatically infer the schema and create an internal training model.

```text
-f "hdfs:///demo/ssn_test2.csv" \
-d "," \
-rd "2018-01-08" \
-ds "ssn_hdfs_file" \
-master yarn \
-deploymode cluster \
-numexecutors 2 \
-executormemory 2g
```

