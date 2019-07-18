# Transform Expressions

## Example

```
./owlcheck \
-ds  "dataset_transform" \
-rd  "2018-01-31" \
-f   "/Users/Documents/file.csv" \
-transform "purch_amt=cast(purch_amt as double)|return_amt=cast(return_amt as double)" 
```

{% hint style="info" %}
Submit an expression to transform a string to a particular type

In this example, transform the purch\_amt column to a double
{% endhint %}

```bash
-transform "purch_amt=cast(purch_amt as double)"
```

{% hint style="info" %}
Example of converting a string to a date
{% endhint %}

```bash
-transform "RECEIVED_DATE=to_date(CAST(RECEIVED_DATE AS STRING), 'yyyyMMdd') as RECEIVED_DATE"
```

