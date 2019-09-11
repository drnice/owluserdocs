---
description: >-
  It would be used when applying a complex condition across multiple
  tables/columns and generally when more flexibility/customization is desired.
---

# Freeform SQL

## Individual statement

#### Syntax

```sql
SELECT * FROM @<dataset_name> <table_alias>
WHERE <filter_expression>
GROUP BY <group_by_expression>
HAVING <having_expression>
```

The base of the statement is given with **@&lt;dataset\_name&gt;** style. In general the &lt;dataset\_name&gt; is the same, where the rule is attached to, but basically you can use any valid dataset name in the expression.

#### Examples

{% tabs %}
{% tab title="Simple rule expression" %}
```scala
opt.dataset = "example_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleNm("is_city_not_null_or_empty")
rule.setRuleValue("select * from @example_ds t where t.amount > '5000'")
rule.setRuleType("SQLF")
rule.setPerc(1.0)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")
```
{% endtab %}

{% tab title="Complex rule expression" %}
```scala
opt.dataset = "unique_rule_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleNm("unique_rule")
rule.setRuleValue("select * from ( select count(*) as cnt, customer_id from @unique_rule_ds group by customer_id ) having cnt > 1")
rule.setRuleType("SQLF")
rule.setPerc(1.0)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")
```
{% endtab %}

{% tab title="RegExp expression" %}
```scala
opt.dataset = "regexp_rule_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleNm("LIKE_rule")
rule.setRuleValue("select * from @regexp_rule_ds.SYMBOL rlike '^ABB+'  ")
rule.setRuleType("SQLG")
rule.setPerc(0.02)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")
```
{% endtab %}
{% endtabs %}

## Join statements

#### A**vailable join types between multiple dataset**

* WHERE tableA.id = tableB.id style
* INNER JOIN
* LEFT &lt;OUTER&gt; JOIN
* RIGHT &lt;OUTER&gt; JOIN

#### **Joining other dataset**

* Getting historical state of the same dataset  
  
  **Syntax:** **@t&lt;n&gt;**,  
  where _n_ parameter means, how many days should we go back in the past at the base dataset \(marked with @&lt;dataset\_name&gt;\)  
  
  **Example:** 

  * **@t1**, will point to the data which was used at yesterday's run
  * **@t4**, will point to the data which was used 4 days ago

* Getting different dataset **Syntax: @&lt;other\_dataset\_name&gt;** 

### WHERE style

{% tabs %}
{% tab title="Look-back dataset" %}
```sql
SELECT * FROM @<dataset_name> <table_alias>, @t1 [<history_table_alias>]
WHERE <join_expression> AND <filter_expression>
```

#### Example

```scala
opt.dataset = "example_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleValue("select * from @example_ds t, @t1  where t.customer_id = t1.customer_id  and t.card_number <> t1.card_number ")
rule.setRuleType("SQLF")
```
{% endtab %}

{% tab title="Different dataset" %}
```sql
SELECT * FROM @<dataset_name> <table_alias>, @<other_dataset_name> [<other_alias>]
WHERE <join_expression> AND <filter_expression>
```

#### Example

```scala
opt.dataset = "example_ds"
opt2.dataset = "other_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleValue("select * from @example_ds t, @other_ds ds2 where t.customer_id = ds2.customer_id  and t.card_number <> ds2.card_number ")
rule.setRuleType("SQLF")
```
{% endtab %}
{% endtabs %}

### LEFT JOIN

**Example**

```scala
opt.dataset = "example_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleNm("not_back2back_days")
rule.setRuleValue(" select * from @example_ds A LEFT OUTER JOIN @t1 B ON A.customer_id = B.customer_id where A.customer_id is not null and B.customer_id is null  ")
rule.setRuleType("SQLF")
rule.setPerc(1.0)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")
```

