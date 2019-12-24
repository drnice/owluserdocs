# Table of contents

* [Owl Analytics](README.md)
* [Why Owl?](why-owl.md)

## Security

* [Owl Security](security/owl-security/README.md)
  * [Authentication With Active Directory LDAP](security/owl-security/authentication-with-active-directory-ldap/README.md)
    * [AD Group to Owl Role Mapping](security/owl-security/authentication-with-active-directory-ldap/ad-group-to-owl-role-mapping.md)
  * [Authentication With Local User Store](security/owl-security/authentication-with-local-user-store/README.md)
    * [Adding Local Users](security/owl-security/authentication-with-local-user-store/adding-local-users.md)
  * [Role Based Access Control \(RBAC\)](security/owl-security/role-based-access-control-rbac.md)
  * [Connection Security](security/owl-security/connection-security.md)
  * [Dataset Security](security/owl-security/dataset-security.md)
  * [Dataset Masking](security/owl-security/dataset-masking.md)

## OwlCheck Examples

* [OwlCheck](owlcheck-examples/owlcheck/README.md)
  * [OwlCheck MySql](owlcheck-examples/owlcheck/owlcheck-mysql.md)
  * [OwlCheck Files](owlcheck-examples/owlcheck/owlcheck-files.md)
  * [OwlCheck Cron](owlcheck-examples/owlcheck/owlcheck-cron.md)
  * [OwlCheck JDBC](owlcheck-examples/owlcheck/owlcheck-jdbc.md)
  * [OwlCheck S3](owlcheck-examples/owlcheck/owlcheck-s3.md)
  * [OwlCheck HDFS](owlcheck-examples/owlcheck/owlcheck-hdfs.md)
  * [OwlCheck Spark](owlcheck-examples/owlcheck/owlcheck-spark.md)
  * [OwlCheck Hive](owlcheck-examples/owlcheck/owlcheck-hive.md)
  * [OwlCheck Validate Source](owlcheck-examples/owlcheck/owlcheck-validate-source.md)
  * [OwlCheck 43M rows](owlcheck-examples/owlcheck/owlcheck-43m-rows.md)
  * [OwlCheck Zeppelin](owlcheck-examples/owlcheck/owlcheck-zeppelin.md)
  * [OwlCheck Kafka](owlcheck-examples/owlcheck/owlcheck-kafka.md)
  * [OwlCheck LinkId](owlcheck-examples/owlcheck/owlcheck-linkid.md)
  * [OwlCheck Back Run](owlcheck-examples/owlcheck/owlcheck-backrun.md)
* [Data Quality Pipelines](owlcheck-examples/data-quality-pipelines/README.md)
  * [Notebook Outlier Example](owlcheck-examples/data-quality-pipelines/notebook-outlier-example.md)
  * [Owl Options API](owlcheck-examples/data-quality-pipelines/owl-options-api.md)
  * [Owl Rules - DQ Pipeline](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/README.md)
    * [Global rules](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/global-rules.md)
    * [SQL based rules](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/README.md)
      * [Simple rule](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/simple-rule.md)
      * [Freeform SQL](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/freeform-sql.md)
      * [Native SQL](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/native-sql.md)
      * [Function](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/function.md)
    * [Data type based rules](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/data-type-based-rules.md)
    * [FAQs](owlcheck-examples/data-quality-pipelines/owl-rules-dq-pipeline/frequently-asked-questions.md)
  * [AWS DataBricks - DQ Pipeline](owlcheck-examples/data-quality-pipelines/aws-databricks-dq-pipeline.md)
  * [Azure DataBricks - DQ Pipeline](owlcheck-examples/data-quality-pipelines/azure-databricks-dq-pipeline.md)
  * [Spark - DQ Pipeline](owlcheck-examples/data-quality-pipelines/spark-dq-pipeline.md)

## Scorecards

* [Dataset Scorecard](scorecards/dataset-scorecard.md)
* [Group Scorecard](scorecards/group-scorecard.md)
* [List View](scorecards/list-view.md)

## Connecting to DBs in Owl Web

* [Owl DB Connection](connecting-to-dbs-in-owl-web/owl-db-connection/README.md)
  * [Connecting to CDH 5.16 Hive SSL/TLS/Kerberos Setup](connecting-to-dbs-in-owl-web/owl-db-connection/connecting-to-cdh-5.16-hive-ssl-tls-kerberos-setup.md)

## DQ Visuals

* [Outliers](dq-visuals/outliers.md)
* [Shapes](dq-visuals/shapes.md)
* [Validate Source](dq-visuals/validate-source.md)
* [Rules](dq-visuals/rules/README.md)
  * [The best DQ rule, is the one you don't have to write](dq-visuals/rules/dq-rule-automation.md)
  * [Creating a Business Rule](dq-visuals/rules/creating-a-business-rule.md)
* [Duplicates](dq-visuals/duplicates.md)
* [Explorer](dq-visuals/explorer.md)
* [Profile](dq-visuals/profile.md)
* [Pattern Mining](dq-visuals/pattern-mining/README.md)
  * [Bloomberg Data](dq-visuals/pattern-mining/bloomberg-data.md)
* [Missing Records](dq-visuals/missing-records.md)

## Labeling / Training

* [Item Labeling](labeling-training/item-labeling.md)
* [Peak vs Off Peak](labeling-training/peak-vs-off-peak.md)

## Graph

* [Process Dependency](graph/process-dependency.md)
* [Dataset Dependency](graph/dataset-dependency.md)

## ARTICLES <a id="creating-a-data-quality-pipeline"></a>

* [Creating a Data Quality Pipeline](creating-a-data-quality-pipeline/creating-a-data-quality-pipeline.md)

## APIs

* [Swagger](apis/swagger.md)
* [Job Server](apis/job-server.md)

## Catalog

* [Catalog](catalog/catalog.md)
* [Cluster Health Report](catalog/cluster-health-report.md)

## Use-Cases

* [Financial FxRate Data](use-cases/financial-fxrate-data.md)
* [Intraday Positions](use-cases/intraday-positions.md)

## Owl Time

* [Owl Time Zone API](owl-time/owl-time-zone-api.md)

## Alerts

* [Email Alerts](alerts/email-alerts.md)

## Troubleshooting

* [Cloudera CLASSPATH](troubleshooting/cloudera-classpath.md)
* [Performance Tuning](troubleshooting/performance-tuning.md)
* [Deploy Mode](troubleshooting/deploy-mode.md)

## Advanced

* [Add Date Column](advanced/add-date-column.md)
* [Behavioral Dimension](advanced/behavioral-dimension.md)
* [Column Deltas](advanced/column-deltas.md)
* [File Look Back](advanced/file-lookback.md)
* [Filter & Filter Not](advanced/filter.md)
* [Multiple Pattern Relationships](advanced/multiple-pattern-combinations.md)
* [Nulls in Datasets](advanced/zero-if-null.md)
* [Reference Checks](advanced/reference-checks.md)
* [Transform Expressions](advanced/transform.md)
* [Prescriptive Personas](advanced/prescriptive-personas.md)

## Multi-Tenant

* [Multi-Tenancy](multi-tenant/multi-tenancy.md)

## Reports

* [Owl Summary Reports](reports/owl-summary-reports.md)

## API

* [JWT](api/jwt.md)
* [Cookie](api/cookie.md)
* [Owl's Scorecard and 9 Dimensions of DQ](owl-dq-screen-shots.md)

