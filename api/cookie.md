---
description: Use cookies file to Run Owl CURL Commands
---

# Cookie



```bash

curl -i -X POST -d username=<username> -d password=<password> http://localhost:9000/login -c cookies.txt

curl -i --header "Accept:application/json" -X GET -b cookies.txt "http://localhost:9000/v2/getsecuritymap"
```

Multi-Tenant without subdomain in URL \(tenant parameter required\):

```bash
curl -i -X POST -d username=<username> -d password=<password> -d tenant=<tenant> -d tenant=public http://localhost:9000/login -c cookies.txt 
 
curl -i --header "Accept:application/json" -X GET -b cookies.txt "http://localhost:9000/v2/getsecuritymap"
```

