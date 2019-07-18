# Add Date Column

## Example

```bash
./owlcheck \
-ds "datataset_date_column" \
-rd "2019-07-01" \
-f "/Users/Downloads/csv2/2019010.csv" \
-adddc
```

{% hint style="info" %}
 Add date column will use the run date supplied and add a date column named **OWL\_RUN\_ID**
{% endhint %}

```bash
-adddc
```

_This is used when you are using datasets that do not contain a date column or a malformed date string_



