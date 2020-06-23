---
description: 'Low Effort, High Stakes Protection'
---

# What is OwlDQ

## From A Business Perspective

The single biggest reason for data quality issues is the amount of time it takes to analyze the data and implement the controls. 

### _**And the biggest issues are the things you would never anticipate \(see below\).**_

| Type | Example |
| :--- | :--- |
| **Invoicing** | _"An ETL update changed our late payments indicator from true/false to 1/0. We were very surprised when many bills were not sent. This caused tremendous headaches to rectify the situation. The rework and reconciliation were very cumbersome."_ |
| **Investment** | _"One of our 200+ reference data feeds introduced a pipe \(\|\) into a position field. The field was defined as VARCHAR so the technical metadata did not change. An upstream provided add this to indicate the long and short legs. Our models went crazy and thought we breached risk limits, we ended up selling out of positions \(losing millions\). Only to uncover the root cause much later that week."_ |
| **Digital** | _"We pull data from many APIs. One platform accounts for 10% of enrichment activities \(i.e. how we monetize our data\). Our auth token accidentally had a daily quota imposed, yet job control said green light \(successful connection\). We still loaded some rows \(1k\), just not entire payloads. This was super nuanced. We literally lost ~10% revenue that month."_ |
| **IoT** | _"We introduced new appliances. They were hooked up and sending valid readings. They were valid values within valid ranges. Turned out, their default setting was rounding the actual values and we were losing precision. Devastating, considering the amount of precision required with blood values."_ |

{% hint style="warning" %}
In each of these cases, the issues were **unanticipated, unexpected, and unintentional.**
{% endhint %}

Owl provides protection for these types of data "surprises". And we all know they happen more than we'd like to admit.

## How can OwlDQ help?

Do more in less time. 

{% hint style="info" %}
On average, 60% of a data worker's time is spent on data quality**.** 
{% endhint %}

Whether you're getting started or applying advanced controls, OwlDQ is [purpose-built](https://docs.owl-analytics.com/what-is-owldq#purpose-built-one-focus) to boost your efforts.

{% hint style="danger" %}
* Data teams overwhelmed with tickets 
* Business users find issues first
* Touchy pipelines get upset with minor updates
* Too busy responding to fire drills to implement new projects
* It takes hours to find out when and why the issue started
{% endhint %}

## **So what is OwlDQ?** 

Think of it as data-driven data monitoring. 

OwlDQ is designed to:

1. Conduct the manual analysis a human would do
2. Provide the suggested data quality checks would write

## How It Works

With a few flicks, Owl will conduct the following steps: 

1. **Collect Data Quality KPIs** -  Probe it from many different perspectives. Interrogate it over several time periods. Measure it across several dimensions.
2. **Generate The Conditions** - Create the data monitoring checks, based on the data points collected. 
3. **Implement Controls** - After several scans, the checks are deployed. You can easily remove or adjust them if needed.

> The answer is in the data if you ask the right questions.

## **Background**

We tried many of the traditional tools and techniques. 

The biggest problem was the amount of time it took to do the analysis and write the checks. 

You get left with half-baked data quality coverage and controls are only added after issues occur.

The result was a never-ending cycle of missed data issues, fire-drills, and a mad scramble to fix it. Fast. All within the context of real-time business operations. 

Traditional approaches, before data saturated every corner of every organization, are very manual. Open a sample or spreadsheet and comb through for analysis \(Table-by-table, column-by-column and item-by-item\). 

Next, manually craft the rules, conditions, tolerances, and thresholds. Then plug-in the scoring, alerting, and reporting. And you wonder why bare-minimum coverage is common.

Now that the surface area of the data in an organization is so much larger, these techniques don't hold up. The primary limitation being a human is required to subjectively do this. 

We wanted a tool that could alert us when data changes occurred, even if we didn't know what those changes might look like.  After all, nobody can predict the future.

Upon evaluating all the commercially available tools, and assessing costs and time of homegrown solutions, it was apparent no tool was available to do the things that we needed and wanted. 

## About

The team comes from a variety of backgrounds. While some spent a decade building technology to detect financial crimes, while others were designing big data infrastructure at fortune 100 companies. 

> _Regardless of the industry or experience, we all faced similar challenges as it related to data quality._



## **Purpose-Built \(One Focus\)**

{% hint style="info" %}
Every feature, visual, and component within Owl is intended to make the analysis and implementation of data quality easier.
{% endhint %}

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring and data quality.  Owl was designed with 4 KPI's in mind:

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl considers scale from two perspectives. Commonly, scale is thought of in terms of processing and compute efficiency.  We agree. Scale is critical from a technical viewpoint. The underlying Owl architecture is designed to work within distributed and elastic environments.  Expertise in this area helped shape the framework. Several engineering team members come from big data backgrounds.  

The other component is usability. Creating a tool that will scale to additional users, outside of a few experts or those with specific skill sets, is a guiding principle. Overly complex configuration, proprietary syntaxes, and unintuitive interfaces added friction.  For these reasons, Owl contains a simple interface available to a wide range of end-users. Collective ownership is critical to avoid bottlenecks within your organization. 

**Unification -** To avoid fragmentation, it was critical to unify all data quality.  OwlDQ will scan files the same way as a database so you can do all in your data monitoring in one place.  Often times you'll have piecemeal or fragmented approaches that lead to data debt and inconsistent controls.  It's also quite challenging to scale and effectively measure data quality without creating a single pane of glass to report and respond from. 

**Measurement -** You can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to cross-cut between different departments, and across varying periods in time. These overarching themes \(speed, scale, unification, measurement\) go hand in hand, in order to create a robust framework.

[See Why Owl For More Information](https://owldq.com/about.html)

## **Core Components**

Owl provides a data quality assessment that scans 9 dimensions. The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes. Owl offers a full DQ suite to cover the unique challenges of each dataset. Complete coverage and consistency drive trust. A single scoring and reporting framework can be activated in a custom DQ pipeline. OwlDQ is horizontally scalable. It can scan data from any location and scale as the data grows in size and complexity. Data quality needs to be abstracted from data ingestion for management to have a single normalized view of data health.  Owl will scan your data with the same frequency, that you load your data.

[See Complete Feature List Breakdown For More Information](https://owldq.com/features.html)

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

[Check out our videos to Learn More](https://owldq.com/videos.html)

## **Who uses OwlDQ?**

* Data Quality
* Data Governance
* Data Engineers
* Data Scientists
* Data Analysts

## **Use cases**

* [ ] [FX Rates](https://docs.owl-analytics.com/use-cases/financial-fxrate-data) \(Outlier Detection\)
* [ ] [Reference Data](https://docs.owl-analytics.com/use-cases/security-reference-data) \(Pattern Detection\)
* [ ] [Cloud Migrations](https://docs.owl-analytics.com/use-cases/copying-or-moving-data) \(Validate Source\)
* [ ] [Wealth Management](https://docs.owl-analytics.com/dq-visuals/duplicates) \(De-duping\) 

More uses cases [available here](https://docs.owl-analytics.com/use-cases/bank-loans)

## **Competitive Landscape** 

![](https://lh5.googleusercontent.com/FtJYdL4983JvNNjhMch5xCmVPUrMHHTyRQcun3JInFYqnRDWtEnIBz9vC8KPEiHXU5AK7zz-93VhKVfX_ugsjcMMNLWl9q9twX2YPRU4izxjop73YKdtJ0TA66zwG3J8JahTIK-d)

In order to avoid getting lost in the latest marketing jargon, a fundamental description is provided under each of the 4 stages.  There are many ways to ingest and transform data; the descriptions are not meant to be exhaustive \(There are easily 30+ software companies in each of the 4 stages\).

## Trust

What it boils down to is the ability to trust the data. What checks and verifications are in place to guarantee data accuracy and completeness? After all, showing someone a housing report with incorrect estimated housing values or a stock report with the wrong stock prices won’t go over well. 

Consistent data monitoring helps you sleep better at night, but also lets the business know they can trust the data. 

## Pricing

\*\*\*\*[**Details**](https://owldq.com/pricing.html)\*\*\*\*

## Learn More

\*\*\*\*[**See a Demo or Request a Trial License**](https://calendly.com/brian-556/calendar)\*\*\*\*

