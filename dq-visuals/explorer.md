# Explorer

### Explore Database Connections and File systems

Use the explorer tab to quickly see which tables are cataloged with Owl \(the square catalog icon\) and which have Owl's quality protection \(the owl icon\).

Below you will see 3/3 database tables have been cataloged with Owl but only 2/3 have an owlcheck.  This means that this particular database schema is 67% protected from future DQ issues.  

![](../.gitbook/assets/owl-explorer.png)

### DQ coverage over time

As you add more datasets to Owl you will see your bar chart increasing over time as well as the donut chart fill in with more coverage.

### Auto Estimator

Before firing off a large ML job it can be helpful to understand the amount of cores and ram that the job requires to run efficiently.  Right sizing jobs is often the best way to get the best performance out of each run.  Click the \[Auto Estimate\] button for quick stats for both sizing and estimated runtime information.

#### Dynamic allocation

Many clusters offer the ability to scale up and down job containers.  If Dynamic allocation is turned on you may not need or desire Owl's recommended num-executors or executor-memory.  However in our testing right sizing the job before executing is both faster and a healthy habit.  Faster because their is less orchestration and context switching while the job is doing work; running out of space allocating more then shuffle to the new container.  Healthier, because it give the user realtime feedback on the cost of each feature and the user can control the cost benefit analysis. 

