---
description: Use JSON Web Tokens to Run Owl CURL Commands
---

# JWT

```bash
TOKEN=$(curl -s -X POST http://localhost:9000/auth/signin -H "Content-Type:application/json" -d "{\"username\":\"<username>\", \"password\":\"<password>\"}" | jq -r '.token')

curl -i -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://localhost:9000/v2/getsecuritymap

```

Multi-Tenant without subdomain in URL \(tenant parameter \[iss\] required\):

```bash
TOKEN=$(curl -s -X POST http://localhost:9000/auth/signin -H "Content-Type:application/json" -d "{\"username\":\"<username>\", \"password\":\"<password>\", \"iss\":\"<tenant>\"}"| jq -r '.token')

curl -i -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://localhost:9000/v2/getsecuritymap

```



Without Headers and jq display:

```bash
curl -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://localhost:9000/v2/getsecuritymap | jq '.' | cat
```



