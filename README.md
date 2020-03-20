# Netlify Dev 404
Trying to replicate the issue discussed here:
Netlify dev server hangs if function returns 404 #695
https://github.com/netlify/cli/issues/695

Clone this project and run `netlify dev`, then run the following `curl` commands.

## GET requests are successful
`time curl --request GET "http://localhost:8888/.netlify/functions/notfoundbug"`
```
BUG
curl --request GET "http://localhost:8888/.netlify/functions/notfoundbug"  0.00s user 0.01s system 48% cpu 0.018 total
```

`netlify dev` output:
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
Response with status 404 in 0 ms.
```

## POST requests hang until aborted
`time curl --request POST --data "{}" "http://localhost:8888/.netlify/functions/notfoundbug"`
```
curl: (52) Empty reply from server
curl --request POST --data "{}"   0.01s user 0.01s system 0% cpu 2:00.03 total
```

`netlify dev` output:
```
Request from ::1: POST /.netlify/functions/notfoundbug
Response with status 404 in 0 ms.
BadRequestError: request aborted
    at IncomingMessage.onAborted (/usr/local/lib/node_modules/netlify-cli/node_modules/raw-body/index.js:231:10)
    at IncomingMessage.emit (events.js:182:13)
    at abortIncoming (_http_server.js:449:9)
    at socketOnClose (_http_server.js:442:3)
    at Socket.emit (events.js:187:15)
    at TCP._handle.close (net.js:610:12)
```