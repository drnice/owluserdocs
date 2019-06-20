---
description: Foreign Exchange Rates
---

# Financial FxRate Data

### Owl Automatically Alerts to Incorrect FX Rate Data without a Single Rule

FX Rate data commonly looks like the below table.  Often you have a TO currency and a FROM currency with the RATE being the multiplier column for conversion.  For example in March you would need to spend $1 US Dollar and 18 US cents to receive $1 Euro.  "In exchange for"  

| TO\_CURR | FROM\_CURR | RATE | DATE |
| :--- | :--- | :--- | :--- |
| USD | EUR | 0.82 | 2019-03-12 |
| EUR | USD | 1.18 | 2019-03-12 |
| USD | YEN | 111.0 | 2019-03-12 |

### 28,000 Currency Pairs

There are roughly 28,000 currency pairs and the exchange rates change throughout the day but at a minimum most banks are concerned with the daily close of the FX Rate.  Now imagine trying to write a rule for each currency pair.  You'd have to know the relationship and adjust a static threshold for each of the 28K pairs every couple days to keep the rule in tact.  Quickly our minds jump to a conclusion that we might be able to solve this with simple math?  We can get closer using averages or percent change formulas but these formulas quickly come up short when some currencies commonly fluctuate more than others.  Ah I got it \(variance\), that college class that I thought I'd never use will finally come in handy. Our minds then quickly graduate from stats 101 to 201 and we could consider the individual variance of every combination.  But even this will only get us so far as time is an important dimension, the length of time or window can often be tricky to calculate.  The problem gets harder when you run your basic stat model and receive a bunch of false positive alerts.  You quickly realize that signal-to-noise ratio is important, confidence factors are important, down-training individual foreign currencies that don't seem to fit you statical model are important.  Knowing if you copied the data incorrectly, truncated 9 levels of precision on the decimal or if the source provider sent the wrong information is important.  Needing the ability to flag exceptions in production on a single currency pair while not flagging the other 27,445 pairs.  Using a feedback loop so that the data steward interactions are captured and learned from Vs. having to take the same corrective action over and over.  What happens when there is a typo in the currency pair or a single pair goes missing?  The answer is that rules don't scale and we need much more than just one off statistical metrics to have a robust and trust worthy DQ program. 

### Consistency

Even when it is possible to deploy a team of smart guys to build a solution to handle this use-case, the question then becomes but what about all my other data, don't I want similar yet different controls on everything?  Especially since FX Rate data by itself doesn't mean that much and is often combined with a number of other datasets to produce value.  What if those datasets aren't accurate either?  But those datasets have very different columns, different relationships and different time windows.  Owl takes an auto-learning approach whereby it interrogates and runs fitness tests against each dataset individually to devise the best statistical and learning approach.  The goal being to provide an automated and elegant way to have consistent controls across all your datasets.     

#### Auto Adapting OwlCheck for FxRate Data

```bash
-ds fx_rate \
-rd $rd \
-dl \
-dlkey TO_CURR,FROM_CURR \
-q "select * from FX_RATE where date = '${rd}'" \
-cxn dbConnName \
-dupe -dupeinc TO_CURR,FROM_CURR -depth 0
```

#### What this OwlCheck Does?

* Automatic correlation and relationship analysis
* Histograming and Segmentation analysis
* Anomaly detection
* Currency pair tracking
* Schema evolution
* Removes 28K static rules
* Duplicate detection for redundant currency pairs



         

