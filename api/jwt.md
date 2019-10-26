---
description: Use JSON Web Tokens to Run Owl CURL Commands
---

# JWT

```bash
TOKEN=$(curl -s -X POST 
http://localhost:9000/auth/signin
 -H "Content-Type:application/json" -d "{\"username\":\"<username>\", \"password\":\"<password>\"}" | jq -r '.token')

curl -i -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" 
http://localhost:9000/v2/getsecuritymap

```

Without Headers and jq display:

curl -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://localhost:9000/v2/getsecuritymap \| jq '.' \| cat





