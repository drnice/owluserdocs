# Outliers

### Numerical Outliers

Kodak Coin!  in 2018 Kodak announced themselves as Kodak coin and witnessed a steep change in their stock price.  Owl automatically captured this event and provided the ability to drill into the item.

![](../.gitbook/assets/owl-outlier-numerical.png)

#### Complex outliers made Simple

Even though Owl uses complex formulas to identify the correct outliers in a dataset, it uses simple terms when displaying them.  If you notice below the change happened gradually, therefore if you only compared avgs or previous values you would not understand the full impact of this price change.  0% changed from yesterday and its moving/trailing avg would have caught up.  

![](../.gitbook/assets/owl-outlier-numerical%20%282%29.png)

### Categorical Outliers

Categorical Outliers are much different than numerical outliers and require separate techniques to automatically capture meaningful anomalies.  The details regarding Owl's methodology and testing can be found below, 3 minute read on the topic.

{% embed url="https://medium.com/owl-analytics/categorical-outliers-dont-exist-8f4e82070cb2" %}

Owl will automatically learn the normal behavior of your Strings and Categorical attributes such as STOCK,OPTION,FUTURE  or state codes such as . MD,NC,D.C.    when a strange pattern occurs such as NYC instead of NY Owl will show this as a categorical outlier.

### Spark DataFrame Example

![](../.gitbook/assets/owl-categorical-outlier.png)

