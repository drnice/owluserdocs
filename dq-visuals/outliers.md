# Outliers

### Numerical Outliers

Kodak Coin!  In 2018 Kodak announced themselves as Kodak coin and witnessed a steep change in their stock price.  Owl automatically captured this event and provided the ability to drill into the item.

![](../.gitbook/assets/owl-outliers.png)

### Categorical Outliers

A 3 minute read on the topic.

{% embed url="https://medium.com/owl-analytics/categorical-outliers-dont-exist-8f4e82070cb2" %}

Owl will automatically learn the normal behavior of your String and Categorical attributes such as STOCK,OPTION,FUTURE or state codes such as MD,NC,D.C. When a strange pattern occurs (e.g NYC instead of NY), Owl will show this as a categorical outlier.

### Spark DataFrame Example

![](../.gitbook/assets/owl-categorical-outlier.png)

