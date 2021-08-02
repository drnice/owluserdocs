# OwlCheck BigQuery

## Example CMD Line

```text
-lib "/opt/owl/drivers/bigquery/bigquery/core/" \
-h <IP_ADDRESS>:5432/postgres \
-master spark://<SPARK_MASTER>:7077 \
-ds samples.loan_customer \
-deploymode client \
-q "select * from samples.loan_customer" \
-rd "2021-08-02" \
-driver "com.simba.googlebigquery.jdbc42.Driver" \
-cxn BigQuery
```

### Steps for the BigQuery Connection

1. **We would use this Simba driver**: com.simba.googlebigquery.jdbc42.Driver
2. **We would make an owl-gcp.json** \(your org auth key in JSON format\)
3. **We would create a JDBC connection** \(for example only do not use this JDBC URL\): jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;ProjectId=;OAuthType=0;OAuthServiceAcctEmail=&lt;1234567890&gt;[-compute@developer.gserviceaccount.com;OAuthPvtKeyPath=/opt/ext/owl-gcp.json;Timeout=86400](mailto:-compute@developer.gserviceaccount.com;OAuthPvtKeyPath=/opt/ext/owl-gcp.json;Timeout=86400)
4. **Requires a path to a JSON file** that contains the service account for authorization. That same file is provided to the Spark session to make a direct to storage connection for maximum parallelism once Core fires up.”

The above and explained there are actually a number of others steps which must be performed to achieve success:

1. **Password for the BigQuery Connector form in Collibra DQ must be a base64 encoded string created from the json file \(see step 3. above\)** and input as password. For example: base64 owl-gcp.json or cat owl-gcp.json \| base64
2. **Check that this JARs exists and is on the path of the Collibra DQ Web UI server** \(eg. &lt;INSTALL\_PATH&gt;/owl/drivers/bigquery/core\). Look at your driver directory location which contains this BigQuery JAR: spark-bigquery\_2.12-0.18.1.jar
3. **Make sure there are all the needed JARs present in &lt;INSTALL\_PATH&gt;/owl/drivers/bigquery/:** _animal-sniffer-annotations-1.19.jar google-api-services-bigquery-v2-rev20201030-1.30.10.jar grpc-google-cloud-bigquerystorage-v1beta1-0.106.4.jar listenablefuture-9999.0-empty-to-avoid-conflict-with-guava.jar annotations-4.1.1.4.jar google-auth-library-credentials-0.22.0.jar grpc-google-cloud-bigquerystorage-v1beta2-0.106.4.jar opencensus-api-0.24.0.jar api-common-1.10.1.jar google-auth-library-oauth2-http-0.22.0.jar grpc-grpclb-1.33.1.jar opencensus-contrib-http-util-0.24.0.jar auto-value-annotations-1.7.4.jar GoogleBigQueryJDBC42.jar grpc-netty-shaded-1.33.1.jar perfmark-api-0.19.0.jar avro-1.10.0.jar google-cloud-bigquery-1.125.0.jar grpc-protobuf-1.33.1.jar protobuf-java-3.13.0.jar checker-compat-qual-2.5.5.jar google-cloud-bigquerystorage-1.6.4.jar grpc-protobuf-lite-1.33.1.jar protobuf-java-util-3.13.0.jar commons-codec-1.11.jar google-cloud-core-1.93.10.jar grpc-stub-1.33.1.jar proto-google-cloud-bigquerystorage-v1-1.6.4.jar commons-compress-1.20.jar google-cloud-core-http-1.93.10.jar gson-2.8.6.jar proto-google-cloud-bigquerystorage-v1alpha2-0.106.4.jar commons-lang3-3.5.jar google-http-client-1.38.0.jar guava-23.0.jar proto-google-cloud-bigquerystorage-v1beta1-0.106.4.jar commons-logging-1.2.jar google-http-client-apache-v2-1.38.0.jar httpclient-4.5.13.jar proto-google-cloud-bigquerystorage-v1beta2-0.106.4.jar conscrypt-openjdk-uber-2.5.1.jar google-http-client-appengine-1.38.0.jar httpcore-4.4.13.jar proto-google-common-protos-2.0.1.jar core google-http-client-jackson2-1.38.0.jar j2objc-annotations-1.3.jar proto-google-iam-v1-1.0.3.jar error\_prone\_annotations-2.4.0.jar google-oauth-client-1.31.1.jar jackson-annotations-2.11.0.jar grpc-alts-1.33.1.jar jackson-core-2.11.3.jar slf4j-api-1.7.30.jar failureaccess-1.0.1.jar grpc-api-1.33.1.jar jackson-databind-2.11.0.jar gax-1.60.0.jar grpc-auth-1.33.1.jar javax.annotation-api-1.3.2.jar threetenbp-1.5.0.jar gax-grpc-1.60.0.jar grpc-context-1.33.1.jar joda-time-2.10.1.jar gax-httpjson-0.77.0.jar grpc-core-1.33.1.jar json-20200518.jar google-api-client-1.31.1.jar grpc-google-cloud-bigquerystorage-v1-1.6.4.jar jsr305-3.0.2.jar_
4. You may get a CLASSPATH conflict regarding the JAR files.
5. Make sure the BigQuery connector Scala version matches your Spark Scala version.[![02%20PM](https://discourse-static.influitive.net/uploads/db_033c9cc6_3cea_4623_b4a8_52ebc3f9e8a1/optimized/2X/d/dfca73373275afb5f063f192a3aa7105caa76bd8_2_286x500.png)](https://discourse-static.influitive.net/uploads/db_033c9cc6_3cea_4623_b4a8_52ebc3f9e8a1/original/2X/d/dfca73373275afb5f063f192a3aa7105caa76bd8.png)





