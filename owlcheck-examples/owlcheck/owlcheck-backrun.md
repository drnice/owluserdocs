---
description: Replay 30 days of data
---

# OwlCheck Back Run

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

