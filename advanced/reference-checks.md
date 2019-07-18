# Reference Checks

## Example

#### Reference Dataset:

Step 1. Define a column to track in a reference dataset using -record and column name

```
-ds reference_dataset,
-rd "2019-07-15" \
-q "select product_type from products" \
-lib "/opt/owl/drivers/postgres/" \
-cxn postgres \
-record "product_types"
```

Step 2. Define the relationship you want to check against the reference dataset

```
-ds "ds1" \
-rd "2018-09-26" \
-q "select * from lake.orders" \
-lib "/opt/owl/drivers/" \
-cxn mysql \
-notin "ds1&type=reference_dataset&product_types"
```

#### Flag

**`-notin ds1&type=reference_dataset&product_types`**

{% hint style="info" %}
This will check if any values from dataset 1 \(ds1\) & column 1 \(type\) are not in the reference dataset \(reference\_dataset\) column \(product\_types\).
{% endhint %}

{% hint style="info" %}
The command is two parts:  
**dataset1&column1=dataset2&column2**
{% endhint %}

_The inverse can be applied to check if a value is in a column by using -in instead of -notin_

This is  applied when there are many reference sets and several combinations for a given dataset. 

