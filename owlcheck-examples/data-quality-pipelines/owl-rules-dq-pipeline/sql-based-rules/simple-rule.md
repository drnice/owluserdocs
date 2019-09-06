---
description: >-
  Simple rules would be applied to filter a condition on a single column in a
  single table.
---

# Simple rule

## Example

In this example you can see how to create a simple SQL rule, with name **simple\_sql\_rule**.

| Code | Description |
| :--- | :--- |
| val rule = new Rule\(\) | Instantiating a Rule object |
| rule.setDataset\(opt.dataset\) | Adding the name of the dataset |
| rule.setRuleNm\("simple\_sql\_rule"\) | Adding the name of the given rule |
| rule.setRuleValue\("startDate &lt; '2011-11-01'"\) | Setting the simple _RULE\_EXPRESSION_ |
| rule.setRuleType\("SQLG"\) | Setting the rule type |
| rule.setPerc\(1.0\) | Setting the percentage |
| rule.setPoints\(1\) | Setting the point |
| rule.setIsActive\(true/false/1/0\)  | Making rule active/inactive |
| rule.setUserNm\("admin"\) | Adding the owner\(username\) |

## Code

{% code-tabs %}
{% code-tabs-item title="example\_simple\_sql\_rule.scala" %}
```scala
import com.owl.core.Owl
import com.owl.core.util.OwlUtils
import com.owl.common.options.OwlOptions
import com.owl.common.{Props, Utils}

import org.junit.{Assert}

import com.owl.common.domain2.Rule

import org.apache.spark.sql.SparkSession
import org.apache.spark.sql.functions._

// Arrange
//----- Init Spark ----- //
def sparkInit(): SparkSession = {
  val sparkSession = SparkSession.builder
    .master("local")
    .appName("test")
    .getOrCreate()
  
  sparkSession
}

val spark = sparkInit()
import spark.implicits._

val headers = "firstName,lastName,startDate"
val source = Seq(
  ("Thomas", "Martinez", "2010-11-01"),
  ("Harry", "Williams", "2012-05-01"),
  ("Ethan", "Davis", "2009-08-01")
)
val arr = headers.split(",")
val df = source.toDF(arr: _*)

val opt = new OwlOptions()
opt.dataset = "simple_sql_rule_ds"
opt.runId = "2019-09-20"
opt.onReadOnly = false
opt.load.pghost = "172.30.2.79:5432/postgres"
opt.load.pguser = "centos"
opt.load.pgpassword = "owlpassword"

val rule = new Rule()
rule.setDataset(opt.dataset)
rule.setRuleNm("simple_sql_rule")
rule.setRuleValue("startDate < '2011-11-01'")
rule.setRuleType("SQLG")
rule.setPerc(1.0)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")

val owl = OwlUtils.OwlContext(df, opt)
  .register(opt)
  .addRule(rule)

// Act
owl.owlCheck()

// Assert
import scala.collection.JavaConversions
val hootRule = JavaConversions.asScalaBuffer(owl.hoot.rules).find(x => rule.getRuleNm.equals(x.getRuleNm)).orNull
Assert.assertNotNull(hootRule)
Assert.assertEquals(66, hootRule.getScore)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Result

### via Code

You can do multiple assertion on the result of the OwlCheck process.  
Using **owl.hoot** parameter will provide access to the execution results, in this case for the rule 

### via UI

![Results of notebook execution on UI](../../../../.gitbook/assets/image%20%2817%29.png)

