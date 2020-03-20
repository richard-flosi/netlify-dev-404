# Netlify Dev 404
Trying to replicate the issue discussed here:
Netlify dev server hangs if function returns 404 #695
https://github.com/netlify/cli/issues/695

In this initial example I'm not able to replicate the issue, but I am seeing the additional requests made looking for the htm/html files.

GET http://localhost:8888/.netlify/functions/notfoundok
returns 404 OK
```
Request from ::1: GET /.netlify/functions/notfoundok
Response with status 404 in 4 ms.
Request from ::1: GET /.netlify/functions/notfoundok.html
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundok.htm
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundok/index.html
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundok/index.htm
Response with status 404 in 1 ms.
```

GET http://localhost:8888/.netlify/functions/notfoundbug
returns 404 BUG
```
Request from ::1: GET /.netlify/functions/notfoundbug
Response with status 404 in 1 ms.
Request from ::1: GET /.netlify/functions/notfoundbug.html
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundbug.htm
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundbug/index.html
Response with status 404 in 0 ms.
Request from ::1: GET /.netlify/functions/notfoundbug/index.htm
Response with status 404 in 1 ms.
```