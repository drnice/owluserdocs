---
description: Replay 30 days of data
---

# OwlCheck Back Run

### How to Replay a Data Test

Many times you will want to see how a dataset plays out over time.  This could be 5 days or 5 months.  Using this slider the tool will automatically create training sets and profiles as well as run any rules or outliers you've put in place.

![](../.gitbook/assets/screen-shot-2021-04-27-at-8.14.28-am.png)

### Quickly Replay 30 days of data, -br 30

Add -br to any owlcheck and replay in time order.  Jan 1, Jan 2, Jan 3...  To do this we need to use the ${rd} variable that owl provides as a run\_date replacement for job control and templates.  Also note that if you run from the cmdline you need to escape "$"s.  so use \${rd}.   If you are running from a Notebook or Java or Scala or the Rest API you do not need to escape the ${rd} variable. 

```bash
./owlcheck \
-ds OWLDB2.NYSE_STOCKS3 -rd "2018-01-14" \
-lib "/opt/owl/drivers/db2/" \
-cxn db2 \
-q "select * from OWLDB2.NYSE_STOCKS where TRADE_DATE = '\${rd}'" \
-br 4
```

### Replay 4 Months of data, -br 4 -tbin MONTH

In situations where your data rolls up into Months you may want to re-run several months of data but not a day at a time.  In this case we will use -br with -tbin

```bash
./owlcheck \
-ds OWLDB2.NYSE_STOCKS3 \
-rd "2018-01-01" \
-q "select * from OWLDB2.NYSE_STOCKS where TRADE_DATE = '\${rd}'" \
-br 4 \
-tbin MONTH \
-lib "/opt/owl/drivers/db2/" \
-cxn db2
```

### Monthly using a range for the entire Month

```bash
./owlcheck \
-ds OWLDB2.NYSE_STOCKS3 \
-rd "2018-01-01" \
-rdEnd "2018-02-01" \
-q "select * from OWLDB2.NYSE_STOCKS where TRADE_DATE >= '${rd}' and TRADE_DATE < '${rdEnd}'" \
-br 4 \
-tbin MONTH
-lib "/opt/owl/drivers/db2/" \
-cxn db2
```

