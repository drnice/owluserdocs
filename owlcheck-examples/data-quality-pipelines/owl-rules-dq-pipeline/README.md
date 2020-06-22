---
description: >-
  In this section you can learn how to work with Rules in Notebooks written in
  Scala.
---

# Owl Rules - DQ Pipeline

## Instantiation

<table>
  <thead>
    <tr>
      <th style="text-align:left">Code</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">val rule = new Rule()</td>
      <td style="text-align:left">Instantiating a Rule object</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setDataset(<em>&lt;DATASET&gt;</em>)</td>
      <td style="text-align:left">Adding the name of the dataset</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setRuleNm(<em>&lt;RULE_NAME&gt;</em>)</td>
      <td style="text-align:left">Adding the name of the given rule</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setRuleValue(<em>&lt;RULE_EXPRESSION&gt;</em>)</td>
      <td style="text-align:left">Setting the simple <em>RULE_EXPRESSION</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setRuleType(<em>&lt;RULE_TYPE&gt;</em>)</td>
      <td style="text-align:left">Setting the rule type</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setPerc(<em>&lt;RULE_PERCENTAGE&gt;</em>)</td>
      <td style="text-align:left">Setting the percentage</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setPoints(<em>&lt;RULE_POINT&gt;</em>)</td>
      <td style="text-align:left">Setting how many points
        <br />will be deducted from total
        <br />for each percentage</td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setIsActive(<em>&lt;RULE_IS_ACTIVE&gt;</em>)</td>
      <td style="text-align:left">
        <p>Making rule active/inactive</p>
        <p>Possible values:</p>
        <ul>
          <li>ACTIVE: <b>1 / true</b>
          </li>
          <li>INACTIVE: <b>0 / false</b>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rule.setUserNm(<em>&lt;RULE_OWNER_USERNAME&gt;</em>)</td>
      <td style="text-align:left">Adding the owner</td>
    </tr>
  </tbody>
</table>

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



