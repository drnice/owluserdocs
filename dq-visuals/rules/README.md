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

One really powerful technique is to access the profile statistics in your rules.  These are typically sub-second operations that do not require scanning or iterating.  There are several cases where SQL struggles to support rules, such as: isNull but not "null count" or nullRatio or nullPercent.  Or having access to types without doing crazy cast\(\) operations.  These are simplified below, i.e. fname.$type == 'String'

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
| **$runId** | $runId = '2020-01-24' | use the ${rd} variable in rules |

<table>
  <thead>
    <tr>
      <th style="text-align:left">Column Level Stat</th>
      <th style="text-align:left">Rule Example</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>.$type</b>
      </td>
      <td style="text-align:left">fname.$type != &apos;String&apos;</td>
      <td style="text-align:left">alert when fname is not a string</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$min</b>
      </td>
      <td style="text-align:left">fname.$min &gt; &apos;apple&apos;</td>
      <td style="text-align:left">lexicographical sort works for strings and numbers</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$minNum</b>
      </td>
      <td style="text-align:left">age.$minNum &gt; 13</td>
      <td style="text-align:left">type casted to a numeric for simple number checks</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$max</b>
      </td>
      <td style="text-align:left">fname.$max &gt; &apos;apple&apos;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$maxNum</b>
      </td>
      <td style="text-align:left">age.$maxNum &gt; 13</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">.<b>$uniqueCount</b>
      </td>
      <td style="text-align:left">id.$uniqueCount != $rowCount</td>
      <td style="text-align:left">alert when the uniqueCount of a field doesn&apos;t match the rowCount</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$uniqueRatio             </b>
      </td>
      <td style="text-align:left">gender.$uniqueRatio between .4 and .6</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$nullRatio</b>
      </td>
      <td style="text-align:left">lname.$nullRatio not between .4 and .6</td>
      <td style="text-align:left">alert when the ratio of nulls no longer falls within acceptable range</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$nullPercent</b>
      </td>
      <td style="text-align:left">lname.$nullPercent not between 40 and 60</td>
      <td style="text-align:left">alert when the percent of nulls no longer falls within acceptable range</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$nullCount</b>
      </td>
      <td style="text-align:left">lname.$nullCount &gt;= 1</td>
      <td style="text-align:left">test for a single null</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$emptyRatio</b>
      </td>
      <td style="text-align:left">nc.$emptyRatio &gt; 0.2</td>
      <td style="text-align:left">alert when the ratio of empties no longer falls within acceptable range</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$emptyPercent</b>
      </td>
      <td style="text-align:left">nc.$emptyPercent &gt; 20</td>
      <td style="text-align:left">alert when the percent of empties no longer falls within acceptable range</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$emptyCount</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$mixedTypeRatio</b>
      </td>
      <td style="text-align:left">nc.$mixedTypeRatio &gt; 0.2</td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$mixedTypePercent</b>
      </td>
      <td style="text-align:left">nc.$mixedTypeRatio &gt; 20</td>
      <td style="text-align:left">
        <p>alert when the percent of mixed data types</p>
        <p>no longer falls within acceptable range.</p>
        <p>i.e. Strings and Ints in the same field</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.$mixedTypeCount</b>
      </td>
      <td style="text-align:left">id.$mixedTypeCount &gt;= 1</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

![](../../.gitbook/assets/colstatrules.png)

Known limitation.  Cannot combine stat rules or distribution rules with regex rules in the same rule.  Example car\__vin rlike '$\[asdf\]\[0-9\]' and car\_vin.$uniqueCount_

### Distribution Rule

There is a common case in DQ where you want to know the distribution of a columns value.  Meaning if you have gender there may be an expectation that 40-60% are males and 40-60% are females if the dataset is large and represents the population.  This can be rather hard or expensive to express in vanilla SQL, but is very easy with the below syntax.

```sql
gender['Male'].$uniquePercent between 40 and 60
```

| Column Value Level | Rule |
| :--- | :--- |
| **.$uniqueCount** | credit\_rating\['FAIR'\].$uniqueCount &gt; 7 |
| **.$uniquePercent** | credit\_rating\['GOOD'\].uniquePercent between 40 and 60 |

![](../../.gitbook/assets/screen-shot-2021-05-10-at-2.24.51-pm.png)

### Quick Tips

If joining more than one data source, make sure both sets of drivers are in the -lib. Or separately supply a -libsrc pointing to the appropriate directory/jar file location.

SQL Freeform uses Spark sql syntax. 

Native SQL uses your native DB syntax. The score is total break records / rows from owlcheck scan. 



