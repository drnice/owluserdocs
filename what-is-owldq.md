# What is OwlDQ

**What is OWL?**

OwlDQ is an intelligent service that automates the heavy lifting involved in data monitoring and data quality. Owl was designed with 4 KPI's in mind:

_Speed, Scale, Unification, and Measurement._  

**Speed -** Owl will check that data is valid, complete, accurate, and consistent.  Data Quality is derived from intuitive clicks, not unnecessary code. Our goal is to deliver DQ in minutes, not days or weeks. 

**Scale -**  Owl approaches scale from two perspectives. Commonly, scale is thought of in terms of processing and compute efficiency.  We agree. Scale is critical from a technical viewpoint. The underlying Owl architecture is designed to work within distributed and elastic environements.  Expertise in this area helped shape the framework. Several engineering team members come from big data backgrounds.  

The other component is usability. Creating a tool that will scale to additional users, outside of a few experts or those with specific skill sets, is a guiding principle. Overly complex configuration, proprietary syntaxes and unintuitive interfaces were considerable pain points with other tools.  For these reasons, Owl contains a simple interface available to a wide range of end-users. Collective ownership is critical to avoid bottlenecks within your organization. 

**Unification -** To avoid silos and fragmented measurement, it was critical to unify all data quality.  Being able to scan files the same way can scan database systems has always been missing from legacy tools.  Often times you'll have piecemeal or fragmented approaches that lead to data debt and inconsistent controls.  It's also quite challenging to scale and effectively measure data quality without creating a single pane of glass to report and respond from. 

**Measurement -** And in the end, you can't manage what you can't measure. It's important to get macro and micro views of data quality, the ability to cross-cut between different departments, and across varying periods in time. These overarching themes go hand in hand, in order to create a robust framework.

**Core Components**

OwlDQ core components - Owl provides a data quality assessment that scans 9 dimensions of a data set to assure the integrity of that data.  The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes. Owl offers a full DQ suite to cover the unique challenges of each dataset. Complete coverage and consistency drive trust. A single scoring and reporting framework with 9  features that can be activated in a custom DQ pipeline. Owl is horizontally scalable, it can scan data from any location and scale as the data grows in size and complexity. Data quality needs to be abstracted from data ingestion for management to have a single normalized view of data health.  Owl will scan your data with the same frequency, that you load your data.  


**Owl Scans 9 dimensions of DQ out of the box**

1. Behavior - imagine a column going null, automatic row count checks  - does you data behave/look/feel the same way it has in the past
2. Rules - assures only values compliant with your data rules are allowed within a data object
3. Outliers - data point that differs significantly from other observations
4. Pattern - recognizing relevant patterns between data examples
5. Source- validating source to target accuracy
6. Record - deltas for a given column
7. Schema - columns drooped
8. Dupes - fuzzy matching to identify entries that have been added multiple times with similar but not exact detail
9. Shapes - infrequent formats

\*\*\*\*

**Use cases**

FX Rates \(Outlier Detection\)

[**https://docs.owl-analytics.com/use-cases/financial-fxrate-data**](https://docs.owl-analytics.com/use-cases/financial-fxrate-data)

Reference Data \(Pattern Detection\)

[**https://docs.owl-analytics.com/use-cases/security-reference-data**](https://docs.owl-analytics.com/use-cases/security-reference-data)

Cloud Migrations \(Validate Source\)

[**https://docs.owl-analytics.com/use-cases/copying-or-moving-data**](https://docs.owl-analytics.com/use-cases/copying-or-moving-data)

Wealth Management \(De-duping\) 

[**https://docs.owl-analytics.com/dq-visuals/duplicates**](https://docs.owl-analytics.com/dq-visuals/duplicates)

**Buyers & Users**

Primary buyers and end-users of OWLDQ \(alignment, where applicable, to use cases\)

* Strategy, Analytics & Deposit Products
* Consumer Credit Risk Management and Loss Forecasting
* Data Analytics, Business Intelligence, and Data Governance Practice
* Commercial Banking Data Analytics
* Data Analytics Strategy & Planning - Global Markets Technology
* Business Analytics / Automation
* Data Quality and Data Governance
* Enterprise Data Management
* Cloud Architecture / Big Data Architecture

\*\*\*\*

**Competitive Landscape**  


![](https://lh5.googleusercontent.com/FtJYdL4983JvNNjhMch5xCmVPUrMHHTyRQcun3JInFYqnRDWtEnIBz9vC8KPEiHXU5AK7zz-93VhKVfX_ugsjcMMNLWl9q9twX2YPRU4izxjop73YKdtJ0TA66zwG3J8JahTIK-d)

In order to avoid getting lost in the latest marketing jargon, a fundamental description is provided under each of the 4 stages.  There are many ways to ingest and transform data; the descriptions are not meant to be exhaustive. Imagine a scenario where data is loaded in either a batch or stream, then joined to another dataset with some column transformations, and finally made viewable in a BI tool for consumption.  But what about quality? What checks and verifications are in place to guarantee data accuracy and completeness? After all, showing someone a housing report with incorrect estimated housing values or a stock report with the wrong stock prices won’t go over well. Figure 2 below has popular company logos overlaid in each stage to bring more context to the discussion. There are easily 30+ software companies in each of the 4 stages.    
  
****

**Background:**

OwlDQ spent about a decade on wall street dealing with DQ problems.  We used rules based tools like IDQ. And ultimately found that we were spending a lot of time writing rules, that were hard to maintain and did not scale. We wanted to change those economics. My group in particular was a team of data scientists, back then they called us quants and we built models to catch things like spoofing, ramping, front-running and insider trading. We really just wanted a simple mechanism to tell us when things are going wrong.  We decided to start using the phd level data science that we were applying to our models, but instead apply it to the data itself. We found that using behavioral analytics we could remove 60% of the rules but also remain adaptive.    
****

**Simple Scenario:**

So, a really simple scenario is, let’s say you have a dataset that has 1 Million rows.  We could write a rule that checks to see if it has less than 1 Million rows. But by next week it grows to 1.1 million and 6 weeks later it grows to 1.5M.  Then suddenly it drops to 1M. The rule still passes but 30% of your data is missing.  


