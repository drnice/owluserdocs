---
description: 'Low Effort, High Stakes Protection'
---

# What is OwlDQ

## From A Business Perspective

Data quality causes significant time, money, and productivity loss.

### _Often times **the biggest issues are the things you least expect** to happen._

| Use Case | Problem |
| :--- | :--- |
| **Invoicing** | Our late payments indicator switched from true/false to 1,0. We were very surprised when many bills were not sent. This caused tremendous headaches to rectify the situation. The rework and reconciliation were very cumbersome.  |
| **Investment** | One of our 200+ reference data feeds introduced a pipe \(\|\) into a position field. The field was defined as VARCHAR so the technical metadata did not change. An upstream provided add this to indicate the long and short legs. Our models went crazy and thought we breached risk limits, we ended up selling out of positions \(losing millions\). Only to uncover the root cause much later that week. |
| **Digital** | We pull data from many APIs. One platform accounts for 10% of enrichment activities \(i.e. how we monetize our data\). Our auth token accidentally had a daily quota imposed, yet job control said green light \(successful connection\). We still loaded _some_ rows \(1k\), just not entire payloads. This was super nuanced. We literally lost ~10% revenue that month. |
| **IoT** | We introduced new appliances. They were hooked up and sending valid readings. They were valid values within valid ranges. Turned out, their default setting was rounding the actual values. Devastating, considering the amount of precision required with blood values. |

{% hint style="warning" %}
In each of these cases, the common theme is they were **unanticipated, unexpected, unintended** changes that caused the actual data issues.
{% endhint %}

You would never imagine some of these scenarios. These were things that never happened before. You certainly wouldn't think to write the appropriate validation checks.

This is where rapid data quality controls can provide more coverage with less effort and protect against significant business-impacting scenarios.

## How can OwlDQ help?

Do more with less. Do more in less time. Whether you're getting started or adding advanced controls, OwlDQ is [purpose-built](https://docs.owl-analytics.com/what-is-owldq#purpose-built-one-focus) to boost your efforts.

{% hint style="danger" %}
* Data teams overwhelmed with tickets 
* Business users find issues first
* Touchy pipelines get upset with minor updates
* Too busy responding to fire drills to implement new projects
* It takes hours to find out when and why the issue started
{% endhint %}

The two most time-consuming aspects of data quality are:

* Analyzing the data
* Writing the checks 

{% hint style="info" %}
On average 60% of a data worker's time is spent on data quality**.** 
{% endhint %}

OwlDQ is designed to:

1. Conduct all the manually-intensive analysis a human would do
2. Then provide the suggested data quality checks a human might try to write

## **What is Data-Driven Data Monitoring?**

While very complex under the hood, the concept is simple. 

We want to use the data to tell us data quality rules that should be implemented. 

* [ ] **Ask The Data Questions** -  Probe it from many different perspectives. Interrogate it over several time periods. Measure it from many angles. 
* [ ] **Use The Answers** - Create data monitoring checks, based on the answers. 
* [ ] **Get Control** - As control checks are brought to your attention and potential DQ issues are surfaced, you can easily add/remove/adjust the checks and scoring.

> The answer is in the data if you ask the right questions.

## **Background**

The team comes from a variety of backgrounds. While some spent a decade building technology to detect financial crimes, while others were designing big data infrastructure at fortune 100 companies. 

> _Regardless of the industry or experience, we all faced similar challenges as it related to data quality._

After evaluating all the commercially available tools, and assessing costs and time of homegrown solutions, it was apparent no tool was available to do the things that we needed and wanted. 

## **Purpose-Built \(One Focus\)**

{% hint style="info" %}
Every feature, visual, and component within Owl is intended to make the analysis and implementation of data quality easier.
{% endhint %}

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring and data quality.  Owl was designed with 4 KPI's in mind:

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl considers scale from two perspectives. Commonly, scale is thought of in terms of processing and compute efficiency.  We agree. Scale is critical from a technical viewpoint. The underlying Owl architecture is designed to work within distributed and elastic environments.  Expertise in this area helped shape the framework. Several engineering team members come from big data backgrounds.  

The other component is usability. Creating a tool that will scale to additional users, outside of a few experts or those with specific skill sets, is a guiding principle. Overly complex configuration, proprietary syntaxes, and unintuitive interfaces added friction.  For these reasons, Owl contains a simple interface available to a wide range of end-users. Collective ownership is critical to avoid bottlenecks within your organization. 

**Unification -** To avoid fragmentation, it was critical to unify all data quality.  OwlDQ will scan files the same way as a database so you can do all in your data monitoring in one place.  Often times you'll have piecemeal or fragmented approaches that lead to data debt and inconsistent controls.  It's also quite challenging to scale and effectively measure data quality without creating a single pane of glass to report and respond from. 

**Measurement -** And in the end, you can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to cross-cut between different departments, and across varying periods in time. These overarching themes \(speed, scale, unification, measurement\) go hand in hand, in order to create a robust framework.

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

What it boils down to is the ability to trust the data. What checks and verifications are in place to guarantee data accuracy and completeness? If you can't trust your data, then what's the point? After all, showing someone a housing report with incorrect estimated housing values or a stock report with the wrong stock prices won’t go over well. 

Consistent data monitoring helps you sleep better at night, but also lets the business know they can trust the data. 

## Pricing

[Details](https://owldq.com/pricing.html)

## Learn More

\*\*\*\*[**See a Demo or Request a Trial License**](https://calendly.com/brian-556/calendar)\*\*\*\*

