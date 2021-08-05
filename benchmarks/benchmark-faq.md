# FAQ

**Performance Recommendations**

Performance is a function of available hardware. 

When running DQ Scans on a Hadoop distribution:

* Check YARN resource manager
* Check limits on queue size
* Contact Platform Administration team on any limitations

When running DQ Scans on Spark standalone \(single node\):

* Check Spark endpoint \(example: http://&lt;IP&gt;:&lt;PORT&gt;\)
* Suggested maximum size on 16 core x 64GB machine: 100 million rows \* 200 columns = 2 billion cells
* If exceeding 2 billion cells, limit the width by selecting certain columns or limit depth with a WHERE clause or a FILTER condition

When running DQ Scans on EKS

* Check your compute pool for available pods
* Check your worker configuration and your Spark operator configuration
* Check minimum and maximum of allowed workers

**How-To**

Increment DQ Scans with gradually increasing limits. Starting with a low level allows you to confirm whether database has proper indexing, skip scanning, or partitioning. Incrementing also allows you to validate security and connectivity quickly. 

* Test 1: Limit 1k rows
* Test 2: Limit 1mm rows
* Test 3: Limit 10mm rows

