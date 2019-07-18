---
description: Run more than one relationship through pattern matching
---

# Multiple Pattern Relationships

## Example

```bash
./owlcheck \
-ds "fpg_multiple" \
-rd "2018-10-04" \

-cxn "postgres" \
-lib   "/opt/owl/drivers/postgres/" \
-q "select * from public.fpg_accounts where d_date = '2018-10-04'" \

-fpgon \
-fpgdc "d_date" \
-fpglb "4" \
-fpgmulti "id,ssn_num=first_name,email|id,ssn_num=first_name,gender|id,ssn_num=last_name" 
```

{% hint style="info" %}
Instead of -fpgkey and -fpgcol

key1=cols1\|keys2=cols2

Enter multiple key=cols combinations separated by a pipe
{% endhint %}

```bash
-fpgmulti "id,ssn_num=first_name,email|id,ssn_num=first_name,gender"

```



