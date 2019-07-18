# Column Deltas

## Example

```
-ds dataset_deltas,
-rd "2019-07-15" \
-q "select * from nyse where run_dt = '2019-07-14'" \
-lib "/opt/owl/drivers/postgres/" \
-cxn postgres \
-record "SYMBOL"
```

{% hint style="info" %}
 A simple way to see if distinct values in a given column are being added or dropped compared to the previous run
{% endhint %}

```
-record "SYMBOL"
```

In this example, if a new symbol is added or dropped it will appear in the Records section of the hoot page.

