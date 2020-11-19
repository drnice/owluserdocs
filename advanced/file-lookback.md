# File Look Back

## Example

```
-ds "demo_lookback" \
-rd "2017-07-29" \
-lib "/opt/owl/drivers/mysql" \
-cxn "mysql" \
-q "select  * from lake.dateseries where DATE_COL = '2017-07-29' " \      
-dc DATE_COL \
-dl \ 
-dlkey sym \
-dllb 4 \
-fllb
```

{% hint style="info" %}
This look back will load your past 4 runs as your historical training set
{% endhint %}

File look back is used with [deep learning ](../dq-visuals/outliers.md#numerical-outliers)or [pattern matching](../dq-visuals/pattern-mining/). In the example above it is used with deep learning.

```
-fllb
```

_**This is often used with files and in conjunction with**_ [_**-adddc**_ ](add-date-column.md)_**in cases where a date column is not in an ideal format or you do not have a date column on the given dataset**_

_Despite the name, this can be used with file or database storage formats._

\_\_

