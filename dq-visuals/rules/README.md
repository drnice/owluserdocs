# Rules

### Rules.  Can't live with them, can't live without them.

Owl takes a strong stance that data should first be profiled, auto-discovered and learned before applying basic rules.  This methodology commonly removes thousands of rules that will never need to be written and evolve naturally overtime.  However there are still many cases to add a simple rule, complex rule or domain specific rule.  Simply search for any dataset and add a rule. You can use the optional Column Name/Category/Description to add meta-data to your rules for future reporting.

![](../../.gitbook/assets/image%20%2848%29.png)

Quick rules are another great way to apply rules at the click of a button in the preview tab.

![](../../.gitbook/assets/image%20%2849%29.png)

### Current Rule Set

Below is a list of one click rules that can be added to any dataset.  It is important to note that Owl often self identifies these columns and automatically provides the proper protection.

* Email
* Zip
* Credit Card
* SSN
* EIN
* State Code
* Phone
* Gender
* IP Address
* Date
* Int
* Double

### Global Shareable Rules

Owl allows a user to define a custom rule and expose it to other users to apply.

### Rule Templates

Create a rule once using our rule template builder and re-use the rule across any column on any dataset.  Owl will substitute the dataset and column that the rule applies to at runtime. This commonly saves hundreds of redundant rules that do the same thing but on different column names.

### Rule Repository

Owl shares all of it's out of the box rules with each user/tenant.  This makes it easy to get started quickly and let the team add common rules for specific use-cases.

![](../../.gitbook/assets/owl-rule-repo.png)

### Query Builder

Query builder will help generate SQL for more complex rules. You can apply to one or two tables \(Table A on left and Table B on right\). For different joins, you can apply a key or matching condition as well. 

![\(Optional\)  Start by searching for table B on the right, to set a key for the join condition](../../.gitbook/assets/screen-shot-2019-09-04-at-12.39.17-pm.png)

![Input conditions and click SQL statement to generate example syntax](../../.gitbook/assets/screen-shot-2019-09-04-at-12.46.02-pm.png)

### Native SQL

![](../../.gitbook/assets/screen-shot-2019-09-04-at-12.57.24-pm.png)

If you have rules already written in Oracle, Sybase, or DB2 syntax - Copy/Paste the rule directly into the Native SQL section. 

### Stat Rules

One really powerful technique is to access the profile statistics in your rules.  These are typically sub-second operations that do not require scanning or iterating.

```sql
select * from @dataset where 
fname.$type != 'String' AND $rowCount < 800
```

| Dataset Level Stat | Rule Example | Description |
| :--- | :--- | :--- |
| **$totalTimeInSeconds** | $totalTimeInSeconds &gt; 25 | alert when DQ job runs longer than 25 seconds. |
| **$totalTimeInMinutes** | $totalTimeInMinutes &gt; 5 | alert when DQ job runs longer than 5 mins. |
| **$totalTimeInHours** | $totalTimeInHours &gt; 1 | alert when DQ job runs longer than 1 hour. |
| **$rowCount** | $rowCount &lt; 9000 | alert when row count less than 9,000 |

| Column Level Stat | Rule Example | Description |
| :--- | :--- | :--- |
| **.$type** | fname.$type != 'String' | alert when fname is not a string |
| **.$min** | fname.$min &gt; 'apple' | lexicographical sort works for strings and numbers |
| **.$minNum** | age.$minNum &gt; 13 | type casted to a numeric for simple number checks |
| **.$max** | fname.$max &gt; 'apple' |  |
| **.$maxNum** | age.$maxNum &gt; 13 |  |
| .**$uniqueCount** | id.$uniqueCount = $rowCount |  |
| **.$uniqueRatio**              | gender.$uniqueRatio between .4 and .6 |  |

### Quick Tips

If joining more than one data source, make sure both sets of drivers are in the -lib. Or separately supply a -libsrc pointing to the appropriate directory/jar file location.

SQL Freeform uses Spark sql syntax. 

Native SQL uses your native DB syntax. The score is total break records / rows from owlcheck scan. 



