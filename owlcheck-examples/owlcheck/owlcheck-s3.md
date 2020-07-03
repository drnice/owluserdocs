# OwlCheck S3

S3 permissions need to be setup appropriately\) \(Needs appropriate driver\) [http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/](http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/) Hadoop AWS Driver hadoop-aws-2.7.3.2.6.5.0-292.jar

```bash
-f "s3a://s3-price-history/testfile.csv" \
-d "," \
-rd "2018-01-08" \
-ds "salary_data_s3" \
-deploymode client \
-lib /home/ec2-user/owl/drivers/aws/
```

### Databricks Utils Or Spark Conf

```bash
val AccessKey = "AKIAJ47QL3SBWY5BOFGA"
val SecretKey = "aaRmxpiiaEpAQT14P2gnGKgeiB+ZivFSrIuTTv2B"
//val EncodedSecretKey = SecretKey.replace("/", "%2F")
val AwsBucketName = "s3-datasets"
val MountName = "kirk"

dbutils.fs.unmount(s"/mnt/$MountName")

dbutils.fs.mount(s"s3a://${AccessKey}:${SecretKey}@${AwsBucketName}", s"/mnt/$MountName")
//display(dbutils.fs.ls(s"/mnt/$MountName"))

//sse-s3 example
dbutils.fs.mount(s"s3a://$AccessKey:$SecretKey@$AwsBucketName", s"/mnt/$MountName", "sse-s3")
```

### Databricks Notebooks using S3 buckets

```bash
val AccessKey = "ABCDED"
val SecretKey = "aaasdfwerwerasdfB"
val EncodedSecretKey = SecretKey.replace("/", "%2F")
val AwsBucketName = "s3-datasets"
val MountName = "abc"

// bug if you don't unmount first
dbutils.fs.unmount(s"/mnt/$MountName")

// mount the s3 bucket
dbutils.fs.mount(s"s3a://${AccessKey}:${EncodedSecretKey}@${AwsBucketName}", s"/mnt/$MountName")
display(dbutils.fs.ls(s"/mnt/$MountName"))

// read the dataframe
val df = spark.read.text(s"/mnt/$MountName/atm_customer/atm_customer_2019_01_28.csv")
```

