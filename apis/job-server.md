---
description: Owl Restful job server
---

# Job Server

### Curl Example

```bash
curl -X POST --data '
{
"file": "/opt/owl/bin/owl-core-trunk-jar-with-dependencies.jar", 
"className": "com.owl.core.cli.Catalog", 
"args": 
    ["-cxn", "-databases", "public", "-driver", "org.postgresql.Driver", "-lib", "/opt/owl/drivers/postgres42/"]
}' 
-H "Content-Type: application/json" localhost:8998/batches
```

### Owl Job Dashboard

![](../.gitbook/assets/owl-job-db.png)

### Configure Multiple Clusters/Agents Per Tenant

Each tenant of Owl can connect and push processing to 1 or more clusters.  Owl is capable of pushing workloads to any of the registered environments \(Agents\) that it knows about. 

![](../.gitbook/assets/owl-tenant-agent%20%281%29.png)

### Add an Agent/Cluster to a Tenant

![](../.gitbook/assets/owl-agent%20%281%29.png)

### Owl Scheduler - Built In

A quick way to schedule jobs is to use Owl's one click scheduler.

![](../.gitbook/assets/owl-schedule.png)

