---
description: >-
  In this section you can learn how to work with Rules in Notebooks written in
  Scala.
---

# Owl Rules - DQ Pipeline

## Definition

| Code | Description |
| :--- | :--- |
| val rule = new Rule\(\) | Instantiating a Rule object |
| rule.setDataset\(opt.dataset\) | Defining the DATASET for the new rule |
| rule.setRuleNm\("simple\_sql\_rule"\) | Setting the name of the given rule |
| rule.setRuleValue\("startDate &lt; '2011-11-01'"\) | Setting the simple _RULE\_EXPRESSION_ |
| rule.setRuleType\("SQLG"\) | Setting the rule type Possible types provided in each sub-page |
| rule.setPerc\(1.0\) | Setting the percentage of |
| rule.setPoints\(1\) |  |
| rule.setIsActive\(1\)  |  |
| rule.setUserNm\("admin"\) |  |



## Rule types

{% page-ref page="sql-based-rules/" %}

{% page-ref page="global-rules.md" %}

{% page-ref page="data-type-based-rules.md" %}

## Requirements

#### Required imports

```scala
import com.owl.core.Owl
import com.owl.core.util.OwlUtils
import com.owl.common.options.OwlOptions
import com.owl.common.{Props, Utils}

import com.owl.common.domain2.Rule

import org.apache.spark.sql.functions._
```

#### SparkSession initialization

DataBricks and other notebook execution frameworks are working with managed/shared spark session, therefor we recommend to use this code snippet in your notebook to initialize the current spark session properly.

```scala
//----- Init Spark ----- //
def sparkInit(): Unit = {
  sparkSession = SparkSession.builder
    .master("local")
    .appName("test")
    .getOrCreate()
}
```

{% hint style="danger" %}
Don't call **spark.stop** at any of your notebooks, otherwise the execution engine will exit immediately!
{% endhint %}

{% hint style="warning" %}
Make sure OwlContext is **already** created before using any method from OwlUtils!
{% endhint %}



