---
description: Use cookies file to Run Owl CURL Commands
---

# Cookie

curl -i -X POST -d username=&lt;username&gt; -d password=&lt;password&gt; [http://localhost:9000/login](http://localhost:9000/login) -c cookies.txt

curl -i --header "Accept:application/json" -X GET -b cookies.txt "[http://localhost:9000/v2/getsecuritymap](http://localhost:9000/v2/getsecuritymap)"

