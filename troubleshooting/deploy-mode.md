---
description: Yarn and Cluster
---

# Deploy Mode

### Deploy Mode Client

```text
--deploy-mode client
```

### Deploy Mode Cluster

```text
--deploy-mode cluster
```

### Job Stuck in ACCEPTED State

yarn.Client: Application report for application\_1557720962505\_0085 \(state: ACCEPTED\)  
yarn.Client: Application report for application\_1557720962505\_0085 \(state: ACCEPTED\)

If running in cluster mode make sure you are passing in the below

```bash
--deploy-mode cluster
--master yarn         # or spark master
-h 123.45.6.77:2181   # host to owl metastore
```

