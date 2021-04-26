---
description: Promoting and moving datasets across environments
---

# Export and Import API

### Step 1

Pass your dataset and tables to the following api call. This endpoint will create a JSON payload

```javascript
http://<url>/v2/get-export?dataset=public.dataset_scan_2&schema=public&tables=owl_catalog,dataset_scan,owl_check_repo
T
```

Examples:

![1 Table](.gitbook/assets/screen-shot-2021-04-26-at-10.02.12-am.png)

![Multiple Tables](.gitbook/assets/screen-shot-2021-04-26-at-10.07.54-am.png)

### Step 2

Run import on the desired environment, passing the output of the previous statement to the body of the request 

```javascript
http://<url>/v2/run-import
```

This would be the body of the POST.

![](.gitbook/assets/screen-shot-2021-04-26-at-10.13.18-am.png)

#### Notes: 

You will want to modify the import payload to check for differences in connections, agents, spark and environment configurations.



#### Get-Exports

Passing in several tables and datasets at once

```javascript
http://<url>/v2/get-exports?dataset=public.dataset_scan_2,public.dataset_scan_1&schema=public&tables=owl_catalog,dataset_scan,owl_check_repo
T
```

![](.gitbook/assets/image%20%2867%29.png)

