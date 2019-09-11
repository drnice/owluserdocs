---
description: Simple check for individual columns
---

# Data type based rules

## Rule types

### Empty check

**Rule type: EMPTYCHECK**  
**Description:** Checking whether the target column has empty values or not

### Null check

**Rule type: NULLCHECK**  
**Description:** Checking whether the target column has _NULL_ values or not

### Date check

**Rule type: DATECHECK**  
**Description:** Checking whether the target column has **only** DATE values or not

### Integer check

**Rule type: INTCHECK**  
**Description:** Checking whether the target column has **only** INTEGER values or not

### Double check

**Rule type: DOUBLECHECK**  
**Description:** Checking whether the target column has **only** DOUBLE values or not

### String check

**Rule type: STRINGCHECK**  
**Description:** Checking whether the target column has **only** STRING values or not.

### Mixed datatype check

**Rule type: DATATYPECHECK**  
**Description:** ---

## Syntax

* **&lt;rule\_type&gt;** - Fixed key to the rule type
* **&lt;column\_name&gt;** - Column to apply the rule
* **&lt;rule\_name&gt;** - Custom name of the rule

```scala
opt.dataset = "example_ds"

val rule = RuleBll.createRule(opt.dataset)
rule.setRuleNm("<rule_name>")
rule.setRuleValue("<column_name>")
rule.setRuleType("<rule_type>")
rule.setPerc(1.0)
rule.setPoints(1)
rule.setIsActive(1)
rule.setUserNm("admin")
```

