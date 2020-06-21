# What is OwlDQ

## **What is OWL?**

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring and data quality. Owl was designed with 4 KPI's in mind:

_Speed, Scale, Unification, and Measurement._  

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl considers scale from two perspectives. Commonly, scale is thought of in terms of processing and compute efficiency.  We agree. Scale is critical from a technical viewpoint. The underlying Owl architecture is designed to work within distributed and elastic environments.  Expertise in this area helped shape the framework. Several engineering team members come from big data backgrounds.  

The other component is usability. Creating a tool that will scale to additional users, outside of a few experts or those with specific skill sets, is a guiding principle. Overly complex configuration, proprietary syntaxes, and unintuitive interfaces added friction.  For these reasons, Owl contains a simple interface available to a wide range of end-users. Collective ownership is critical to avoid bottlenecks within your organization. 

**Unification -** To avoid fragmentation, it was critical to unify all data quality.  OwlDQ will scan files the same way as a database so you can do all in your data monitoring in one place.  Often times you'll have piecemeal or fragmented approaches that lead to data debt and inconsistent controls.  It's also quite challenging to scale and effectively measure data quality without creating a single pane of glass to report and respond from. 

**Measurement -** And in the end, you can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to cross-cut between different departments, and across varying periods in time. These overarching themes \(speed, scale, unification, measurement\) go hand in hand, in order to create a robust framework.

## **Core Components**

OwlDQ core components - Owl provides a data quality assessment that scans 9 dimensions of a data set to assure the integrity of that data.  The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes. Owl offers a full DQ suite to cover the unique challenges of each dataset. Complete coverage and consistency drive trust. A single scoring and reporting framework with 9  features that can be activated in a custom DQ pipeline. Owl is horizontally scalable, it can scan data from any location and scale as the data grows in size and complexity. Data quality needs to be abstracted from data ingestion for management to have a single normalized view of data health.  Owl will scan your data with the same frequency, that you load your data.

**Owl Scans 9 dimensions of DQ out of the box**

1. Behavior - Metadata and technical data monitoring checks
2. Rules - SQL-based rules engine
3. Outliers - Large spikes or drops in values
4. Pattern - Cross-column categorical anomalies 
5. Source - Source to target reconcilliation
6. Record - Deltas for a given column
7. Schema - Columns added or dropped. 
8. Dupes - Fuzzy matching, Identify similar but not exact entries
9. Shapes - Typos, Formatting Anomalies

## **Use cases**

FX Rates \(Outlier Detection\)

[**https://docs.owl-analytics.com/use-cases/financial-fxrate-data**](https://docs.owl-analytics.com/use-cases/financial-fxrate-data)

Reference Data \(Pattern Detection\)

[**https://docs.owl-analytics.com/use-cases/security-reference-data**](https://docs.owl-analytics.com/use-cases/security-reference-data)

Cloud Migrations \(Validate Source\)

[**https://docs.owl-analytics.com/use-cases/copying-or-moving-data**](https://docs.owl-analytics.com/use-cases/copying-or-moving-data)

Wealth Management \(De-duping\) 

[**https://docs.owl-analytics.com/dq-visuals/duplicates**](https://docs.owl-analytics.com/dq-visuals/duplicates)

## **Who uses OwlDQ?**

* Data Quality
* Data Governance
* Data Engineers
* Data Scientists
* Data Analysts

## **Competitive Landscape** 

![](https://lh5.googleusercontent.com/FtJYdL4983JvNNjhMch5xCmVPUrMHHTyRQcun3JInFYqnRDWtEnIBz9vC8KPEiHXU5AK7zz-93VhKVfX_ugsjcMMNLWl9q9twX2YPRU4izxjop73YKdtJ0TA66zwG3J8JahTIK-d)

In order to avoid getting lost in the latest marketing jargon, a fundamental description is provided under each of the 4 stages.  There are many ways to ingest and transform data; the descriptions are not meant to be exhaustive. Imagine a scenario where data is loaded in either a batch or stream, then joined to another dataset with some column transformations, and finally made viewable in a BI tool for consumption.  But what about quality? What checks and verifications are in place to guarantee data accuracy and completeness? After all, showing someone a housing report with incorrect estimated housing values or a stock report with the wrong stock prices won’t go over well. Figure 2 below has popular company logos overlaid in each stage to bring more context to the discussion. There are easily 30+ software companies in each of the 4 stages.  ****   


