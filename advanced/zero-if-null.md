# Nulls in Datasets

## Example

```
./owlcheck \
-ds "datataset_date_column" \
-rd "2019-07-01" \
-f "/Users/Downloads/csv2/2019010.csv" \
-zfn \
-nulls "N.A."   
```

Zero if null will replace null values with zero

```
-zfn  
```

To replace characters that represent a null to actual null values

```
-nulls "N.A."
```







