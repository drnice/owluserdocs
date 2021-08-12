# Completeness Report

Completeness commonly means what percentage of your data is empty or null.  The confusion often comes when you consider the context of completeness.  Completeness of a column?  Completeness of a dataset \(file or table\)? Completeness of a collection of tables or business unit?  And even worse... completeness over time.

Fortunately the Collibra DQ Completeness Report covers all of these dimensions, allowing the user to generate a report that answers almost any completeness question.  We have also found that volume weighted completeness is likely a better metric than average completeness in a rollup scenario.

### Report Builder

![](../.gitbook/assets/screen-shot-2021-08-12-at-5.26.43-pm.png)

When looking at Completeness over time you may need to differentiate between the time when the DQ job ran \(update time\) or the date/time the data represents \(run date\).  For example I load stock data today but the data I loaded was for last week. 

### Column Completeness vs Dataset Completeness

![](../.gitbook/assets/screen-shot-2021-08-12-at-4.04.53-pm.png)

