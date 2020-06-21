---
description: 'Who, What, How and Why'
---

# What is OwlDQ

## **Mission**

To make data quality easier. 

## How can OwlDQ help?

{% hint style="info" %}
On average 60% of a data worker's time is spent analyzing data quality**.** 
{% endhint %}

The two most time-consuming aspects are:

* Analyzing the data
* Writing the checks 

OwlDQ is designed to:

1. Conduct all the manually-intensive analysis a human might do
2. Then provide the suggested data quality checks a human might try to write

We call it "[Low Effort, High Stakes Protection](https://www.youtube.com/watch?v=S5cI3mYyCFw&t=26s)". 

## **Background**

The team is comprised of a variety of backgrounds and skillsets. While some spent a decade using technology to detect financial crimes, others were tracking cyber fraud, and others were designing big data infrastructure at fortune 100 companies. 

_Regardless of the industry or experience, we all faced similar challenges as it related to data quality._

{% hint style="info" %}
* Data teams overwhelmed with tickets 
* Business users find issues first
* Touchy pipelines get upset with minor updates
* Too busy responding to fire drills to implement new projects
* It takes hours to find out when and why the issue started
{% endhint %}

After evaluating all the commercially available tools, and assessing costs and time of homegrown solutions, it was apparent no tool was available to do the things that we needed and wanted. 

## **What is Data-Driven Data Monitoring?**

While very complex under the hood, the concept is simple. 

We want to use the data to tell us data quality rules that should be implemented. 

* [ ] **Ask The Data Questions** -  Probe it from many different perspectives. Interrogate it over several time periods. Measure it from many different angles. 
* [ ] **Use these Answers** - Create data monitoring checks, based on the answers. 
* [ ] **Implement Controls** - Control checks will be brought to your attention. Potential issues will be surfaced. You can easily add/remove checks, adjust sensitivity, and scoring all with a few clicks.

The answer is in the data if you ask the right questions. 

## **Core Tenets**

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring and data quality. Owl was designed with 4 KPI's in mind:

_Speed, Scale, Unification, and Measurement._  

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl considers scale from two perspectives. Commonly, scale is thought of in terms of processing and compute efficiency.  We agree. Scale is critical from a technical viewpoint. The underlying Owl architecture is designed to work within distributed and elastic environments.  Expertise in this area helped shape the framework. Several engineering team members come from big data backgrounds.  

The other component is usability. Creating a tool that will scale to additional users, outside of a few experts or those with specific skill sets, is a guiding principle. Overly complex configuration, proprietary syntaxes, and unintuitive interfaces added friction.  For these reasons, Owl contains a simple interface available to a wide range of end-users. Collective ownership is critical to avoid bottlenecks within your organization. 

**Unification -** To avoid fragmentation, it was critical to unify all data quality.  OwlDQ will scan files the same way as a database so you can do all in your data monitoring in one place.  Often times you'll have piecemeal or fragmented approaches that lead to data debt and inconsistent controls.  It's also quite challenging to scale and effectively measure data quality without creating a single pane of glass to report and respond from. 

**Measurement -** And in the end, you can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to cross-cut between different departments, and across varying periods in time. These overarching themes \(speed, scale, unification, measurement\) go hand in hand, in order to create a robust framework.

## **Core Components**

Owl provides a data quality assessment that scans 9 dimensions. The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes. Owl offers a full DQ suite to cover the unique challenges of each dataset. Complete coverage and consistency drive trust. A single scoring and reporting framework can be activated in a custom DQ pipeline. OwlDQ is horizontally scalable. It can scan data from any location and scale as the data grows in size and complexity. Data quality needs to be abstracted from data ingestion for management to have a single normalized view of data health.  Owl will scan your data with the same frequency, that you load your data.

**9 Dimensions of DQ**

1. Behavior - Metadata and technical data monitoring checks
2. Rules - SQL-based rules engine
3. Outliers - Large spikes or drops in values
4. Pattern - Cross-column categorical anomalies 
5. Source - Source to target reconciliation
6. Record - Deltas for a given column
7. Schema - Columns added or dropped. 
8. Dupes - Fuzzy matching, Identify similar but not exact entries
9. Shapes - Typos, Formatting Anomalies

[Check out our videos  to Learn More](https://owldq.com/videos.html)

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

In order to avoid getting lost in the latest marketing jargon, a fundamental description is provided under each of the 4 stages.  There are many ways to ingest and transform data; the descriptions are not meant to be exhaustive \(There are easily 30+ software companies in each of the 4 stages\).

## Trust

What checks and verifications are in place to guarantee data accuracy and completeness? After all, showing someone a housing report with incorrect estimated housing values or a stock report with the wrong stock prices won’t go over well.   


