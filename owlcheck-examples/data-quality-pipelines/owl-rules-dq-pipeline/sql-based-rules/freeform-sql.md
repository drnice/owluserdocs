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

#### Example **snippet**

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

#### Syntax - with look-back 

```sql
SELECT * FROM @<dataset_name> <table_alias>, @t1 [<history_table_alias>]
WHERE <join_expression> AND <filter_expression>
```

#### Example **snippet**

```scala
opt.dataset = "example_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleValue("select * from @example_ds t, @t1  where t.customer_id = t1.customer_id  and t.card_number <> t1.card_number ")
rule.setRuleType("SQLF")
```

#### Syntax - with different dataset

```sql
SELECT * FROM @<dataset_name> <table_alias>, @<other_dataset_name> [<other_alias>]
WHERE <join_expression> AND <filter_expression>
```

#### Example **snippet**

```scala
opt.dataset = "example_ds"
opt2.dataset = "other_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleValue("select * from @example_ds t, @other_ds ds2 where t.customer_id = ds2.customer_id  and t.card_number <> ds2.card_number ")
rule.setRuleType("SQLF")
```

### INNER JOIN

### LEFT JOIN

### RIGHT JOIN

