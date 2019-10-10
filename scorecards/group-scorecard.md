# Group Scorecard

## Visually and logically group datasets together to create a heat-map of blindspots.

Similarly to job control and build frameworks like Jenkins, we always want to know the health of our datasets. Did it recently fail? Does it commonly fail on Mondays? What is the aggregate or composite score for multiple datasets? Owl allows you to define scheduled health checks that depend on the success/failure status of any number of datasets. This protects the downstream process consumers from pulling erroneous data into their models.

![](../.gitbook/assets/owl-group-scorecard.png)

