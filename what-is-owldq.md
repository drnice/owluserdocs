---
description: 'Low Effort, High Stakes Protection'
---

# What is OwlDQ

## From A Business Perspective

{% hint style="info" %}
On average, 60% of a data worker's time is spent on data quality**.** It takes a tremendous amount of time to do the analysis and write the checks. 
{% endhint %}

This friction leads to patchy and incomplete coverage and leaves your organization vulnerable to data quality issues.  

### _**And the biggest issues are the things you never expect \(see below\).**_

| Type | Example |
| :--- | :--- |
| **Invoicing** | _"An ETL update changed our late payments indicator from true/false to 1/0. We were very surprised when many bills were not sent. The rework and reconciliation were super painful."_ |
| **Investment** | _"One of our 200+ reference data feeds introduced a pipe \(\|\) into a position field. The field was defined as VARCHAR so the technical metadata did not change. An upstream provided add this to indicate the long and short legs. Our models went crazy and thought we breached risk limits, we ended up selling out of positions \(losing millions\). Only to uncover the root cause much later that week."_ |
| **Digital** | _"We pull data from many APIs. One platform accounts for 10% of enrichment activities \(i.e. how we monetize our data\). Our auth token accidentally had a daily quota imposed, yet job control said green light \(successful connection\). We still loaded some rows \(1k\), just not entire payloads. This was super nuanced. We literally lost ~10% revenue that month."_ |
| **IoT** | _"When we introduced new meters, they were hooked up and sending valid readings. They were valid values within valid ranges. Turned out, their default setting was rounding the actual values and we were losing precision. Devastating, considering the amount of precision required with blood values."_ |

{% hint style="warning" %}
In each of these cases, the issues were **unanticipated, unexpected, and unintentional.**
{% endhint %}

Owl provides protection for these types of data "surprises".  We all know they happen more than we would like.

## How can OwlDQ help?

Do more in less time. 

Whether you're getting started or applying advanced controls, OwlDQ is [purpose-built](https://docs.owl-analytics.com/what-is-owldq#purpose-built-one-focus) to boost your efforts.

{% hint style="danger" %}
* Data teams overwhelmed with tickets 
* Business users find issues first
* Touchy pipelines get upset with minor updates
* Too busy responding to fire drills to implement new projects
* It takes hours to find out when and why the issue started
{% endhint %}

## **So What is OwlDQ?** 

Think of it as data-driven data monitoring. 

OwlDQ is designed to:

1. Conduct the manual analysis a human would do
2. Provide the data quality checks a human would write

## How Do You Get Started \(4 step process\)? 

Getting started the easy way. 

{% tabs %}
{% tab title="DQ Now" %}
#### Critical Control Layer

* Always-On Profiling
* Metadata Monitoring
* Rapid Rules \(auto-Applied\) 

_Fast to implement, must-have protection, no code._
{% endtab %}

{% tab title="DQ Discover" %}
#### Analysis Layer

* Format Finder
* Outlier Detect
* Cross-Column Basket Analyzer

 _Auto-discovery and deeper analysis to uncover hard-to-find data quality issues._
{% endtab %}

{% tab title="DQ Select" %}
#### Guided Layer

* B.Y.O.R. \(bring your own rules\)
* Reconciliation
* Fuzzy Matching

_Blend human input to perform precise checks._
{% endtab %}

{% tab title="DQ Deploy" %}
#### Operational Layer

* Report Repo
* Scheduler 
* Alert Center
* Security Control 

_All the things you need to make it work for you._
{% endtab %}
{% endtabs %}

## How Does it Work?

With a few flicks, Owl will conduct the following steps: 

1. **Collect Data Quality KPIs** -  Probe the data from many different perspectives. Interrogate it over several time periods. Measure it across several dimensions.
2. **Generate The Conditions** - Under the hood Owl creates SQL-based data monitoring checks, based on the data points collected. 
3. **Implement The Controls** - After several scans, the checks are deployed. You can easily remove or adjust them as needed.

> The answer is in the data if you ask the right questions.

## Background

The team comes from a variety of backgrounds. While some spent a decade building technology to detect financial crimes, others were designing big data infrastructure at fortune 100 companies. 

> _Regardless of the industry or experience, we all faced similar challenges as it related to data quality._

These unique vantage points have allowed us to understand the most common data quality challenges organizations are facing.

## What Did We Notice? 

We tried many of the traditional tools and techniques. The biggest problem was always the amount of time it took to do everything needed to implement and maintain data quality controls. 

You get left with half-baked data quality coverage and the right controls are added only after issues occur.

It turned out teams were doing the same tasks for every dataset and for each department, building the exact same tools over and over. 

{% hint style="danger" %}
The result was a never-ending cycle of data issues, fire-drills, and a mad scramble to fix it. Fast. All within the context of real-time business operations. 
{% endhint %}

## Traditional Approach

Traditional approaches are very manual. 

Start by opening a sample or spreadsheet and conduct analysis \(Table-by-table, column-by-column, query-by-query, and item-by-item\). 

Next, manually craft the rules, conditions, tolerances, and thresholds. 

Then stitch together the dashboards, scoring, workflows, alerts, and reporting. And you wonder why bare-minimum coverage is common.

{% hint style="warning" %}
You're only as good as the rules you thought to write. 
{% endhint %}

#### Fast Forward

Now that the surface area of the data in an organization is so much larger, these techniques don't hold up. 

## What Did We Need?

What we needed didn't exist. As lifelong data enthusiasts, we wanted a tool that could alert us when data changes occurred without complicated setup and lengthy analysis.  We sought something that could work on big, medium, and small data and across all storage formats. Upon evaluating all the commercially available tools, and assessing costs and time of homegrown solutions, there were no great options.

## **Purpose-Built \(One Focus\)**

{% hint style="info" %}
Every feature, visual, and component within Owl is intended to make the analysis and implementation of data quality easier.
{% endhint %}

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring. Owl was designed with 4 KPI's in mind:

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl considers scale from two perspectives. From a technical viewpoint, OwlDQ is designed to work in distributed and elastic environments. It can scan any data from any location. The other piece is usability. Creating a tool that will scale to additional users, outside of a few experts, is equally important.  

**Unification -**   OwlDQ will scan files the same way as a database so you can do all in your data monitoring in one place, rather than piecemeal approaches.  Data quality needs to be unified to have a single normalized view of data health.

**Measurement -** You can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to compare between different departments, and time periods. 

[See Why Owl For More Information](https://owldq.com/about.html)

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

## **Core Components**

Owl provides a data quality assessment that scans 9 dimensions. Owl offers a full DQ suite to cover the unique challenges of each dataset. 

[See Complete Feature List Breakdown For More Information](https://owldq.com/features.html)

**9 Dimensions of DQ**

1. Behavior - Metadata monitoring
2. Rules - SQL-based rules engine
3. Outliers - Anomalous records
4. Pattern - Cross-column categorical anomalies 
5. Source - Source to target reconciliation
6. Record - Deltas for a given column\(s\)
7. Schema - Columns added or dropped
8. Dupes - Fuzzy matching, Identify similar but not exact entries
9. Shapes - Typos, Formatting Anomalies

[Check out our videos to Learn More](https://owldq.com/videos.html)

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

