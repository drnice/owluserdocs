# Behavioral Dimension

## Example

```
-ds "dataset_behavioral_dimension" \
-rd "2019-07-15" \
-d "," \
-f "/Users/brian/Documents/synthetic3.csv" \
-bd "labcode"
```

{% hint style="info" %}
Track the counts for distinct columns or relationships for behavioral analytics on individual column components
{% endhint %}

```
-bd "labcode"
```

Go beyond just tracking distinct values per the entire column. 

For example, if you had a column \(or multiple columns\) that typically contained 5 values and each of those values typically represented 20% of the column.  

**ColumnA**  
a -&gt; 20  
b -&gt; 20  
c -&gt; 20  
d -&gt; 20  
e -&gt; 20

Consider the row count remained 100 and the total distinct values remained 5, but suddenly the proportion of a given value changed drastically.

**ColumnA**  
a -&gt; 1  
b -&gt; 39  
c -&gt; 20  
d -&gt; 20  
e -&gt; 20

Behavioral dimension would flag that ColumnA value a is represented much less than normal and value b is represented much more than normal.

