# Intraday Positions

It is common for financial organizations to receive a steady stream of files that have hourly or minutely data.  The files might trail the market in a near real-time fashion.  Below is an example

```text
--positions/
   |--2019/
     |--01/
       |--22/
         position_2019_01_22_09.csv
         position_2019_01_22_10.csv
         position_2019_01_22_11.csv
         position_2019_01_22_12.csv
```

### File Contents @ 9am

| TIME | COMPANY | TICK | SIDE | QTY |
| :--- | :--- | :--- | :--- | :--- |
| 2019-01-22 09:00 | T&G | xyz | LONG | 300 |
| 2019-01-22 09:00 | Fisher | abc | SHORT | 20 |
| 2019-01-22 09:00 | TradeServ | def | LONG | 120 |

### File Contents @ 10am

| TIME | COMPANY | TICK | SIDE | QTY |
| :--- | :--- | :--- | :--- | :--- |
| 2019-01-22 10:00 | T&G | xyz | LONG | 280 |
| 2019-01-22 10:00 | BlackTR | ghi | SHORT | 45 |

Notice that during the day you may or may not have a position for every company recorded.  We need a way to link the "company" to its position throughout the day but not alert in cases where they simply did not trade or adjust their position.  Owl offers real-time outlier detection for this scenario \(see code snippet below\).  We also need to make sure that each companies position is only represented once per file \(per hour in this case\).  Owl offers duplicate detection \(see code snippet below\).

### Owl DQ Pipeline

```scala
here
```

### DQ Coverage for Position data

* Schema Evolution
* Profiling
* Correlation Analysis
* Segmentation
* Outlier Detection
* Duplicate Detection
* Pattern Mining

