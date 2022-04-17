<!-- DELETE EVERYTHING ABOVE THIS LINE -->

# Coinserver Description

This package exposes endpoints and provides a web interface to emulate random chance coin flip events in the following ways:

1. Flip one coin - returns result of a coin flip
2. Flip many coins - returns the results of many coin flips with a summary
3. Guess a coin flip and - returns the result of a flip and guess match

# Coinserver Installation

Run `npm install` inside the package root directory.

This package was buid using Node.js LTS (16.x).
Other package dependency and version information can be found in `package.json`.

# Coinserver Runtime Documentation
```
node server.js [options]

--port, -p	Set the port number for the server to listen on. Must be an integer
            between 1 and 65535. Defaults to 5000.

--debug, -d If set to true, creates endlpoints /app/log/access/ which returns
            a JSON access log from the database and /app/error which throws 
            an error with the message "Error test successful." Defaults to 
            false.

--log, -l   If set to false, no log files are written. Defaults to true.
            Logs are always written to database.

--help, -h	Return this message and exit.
```

# Coinserver API Documentation

## Endpoints

### /app/ (GET)

#### Request cURL

```
curl http://localhost:5000/app/
```

#### Response body

```
{"message":"Your API works! (200)"}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 35
ETag: W/"23-KNmhzXgQhtEE5ovS3fuLixylNK0"
Date: Thu, 07 Apr 2022 15:07:49 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/flip/one (GET)

#### Request cURL

```
curl http://localhost:5000/app/flip/one
```

#### Response body

```
{"result":"heads"}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 18
ETag: W/"12-LUQPHBtW+sQqHvQ4HD7ph4ZTpW4"
Date: Sun, 17 Apr 2022 01:13:27 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/flip/coins/:number/ (GET)

#### Request cURL

```
curl http://localhost:5000/app/flip/coins/3
```

#### Response body

```
{"raw":["heads","heads","tails"],"summary":{"heads":2,"tails":1}}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 55
ETag: W/"37-nUcPqHO9FfbI8DRbRY5p3lRI1i4"
Date: Sun, 17 Apr 2022 01:17:07 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/flip/call/:guess/ (GET)

#### Request cURL

```
curl http://localhost:5000/app/flip/call/heads/
```

#### Response body

```
{"call":"heads","flip":"tails","result":"lose"}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 47
ETag: W/"2f-7jHpBxeRlMwmX45a5nEiITPVllI"
Date: Sun, 17 Apr 2022 01:19:27 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/flip/call/ (POST)

#### Request cURL

```
curl -X POST -H 'Content-Type: application/json' -d '{"guess":"heads"}' http://localhost:5000/app/flip/call/
```

#### Response body

```
{"call":"heads","flip":"heads","result":"win"}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 46
ETag: W/"2e-U/q8iZ4JKqczXPIvtwiVRpEFlRc"
Date: Thu, 07 Apr 2022 16:30:07 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/flip/coins/ (POST)

#### Request cURL

```
curl -X POST -H 'Content-Type: application/json' -d '{"number":"30"}' http://localhost:5000/app/flip/coins/`
```

#### Response body

```
{"raw":["heads","heads","heads","tails","heads","heads","tails","tails","tails","heads","heads","heads","heads","heads","heads","tails","tails","heads","heads","heads","heads","heads","heads","heads","tails","heads","tails","heads","tails","heads"],"summary":{"heads":21,"tails":9}}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 283
ETag: W/"11b-9dPTqGfngSPFEOq4loChIlpdSIE"
Date: Thu, 07 Apr 2022 15:23:35 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/log/access/ (GET)

#### Request cURL

```
curl http://localhost5555/app/log/access
```

#### Response body

```
{"id":0,"time":1650068280212,"remoteaddr":"::1","remoteuser":"undefined","method":"GET","url":"/app/flip/one","protocol":"http","httpversion":"1.1","secure":"false","status":"200","referer":"undefined","useragent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.88 Safari/537.36"},{"id":1,"time":1650068281330,"remoteaddr":"::1","remoteuser":"undefined","method":"GET","url":"/app/flip/one","protocol":"http","httpversion":"1.1","secure":"false","status":"200","referer":"undefined","useragent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.88 Safari/537.36"}
```

#### Response headers

```
HTTP/1.1 200 OK
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Type: application/json; charset=utf-8
Content-Length: 28586
ETag: W/"6faa-VHgcU83OpHX6+brFLgYOKwxwMow"
Date: Sun, 17 Apr 2022 01:20:56 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### /app/error/ (GET)

#### Request cURL

```
curl http://localhost:5000/app/error/
```

#### Response body

```
HTTP/1.1 500 Internal Server Error
X-Powered-By: Express
Access-Control-Allow-Origin: *
Content-Security-Policy: default-src 'none'
X-Content-Type-Options: nosniff
Content-Type: text/html; charset=utf-8
Content-Length: 1275
Date: Sun, 17 Apr 2022 01:22:19 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

#### Response headers

```
Error: Error test successful.<br> &nbsp; &nbsp;at /Users/iwa332/VSCode/a05-iadams749/index.js:108:13<br> &nbsp; &nbsp;at Layer.handle [as handle_request] (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/layer.js:95:5)<br> &nbsp; &nbsp;at next (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/route.js:137:13)<br> &nbsp; &nbsp;at Route.dispatch (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/route.js:112:3)<br> &nbsp; &nbsp;at Layer.handle [as handle_request] (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/layer.js:95:5)<br> &nbsp; &nbsp;at /Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/index.js:281:22<br> &nbsp; &nbsp;at Function.process_params (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/index.js:341:12)<br> &nbsp; &nbsp;at next (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/index.js:275:10)<br> &nbsp; &nbsp;at /Users/iwa332/VSCode/a05-iadams749/index.js:94:5<br> &nbsp; &nbsp;at Layer.handle [as handle_request] (/Users/iwa332/VSCode/a05-iadams749/node_modules/express/lib/router/layer.js:95:5)
```

### /app/log/error/ (GET)

_Not yet implemented_

#### Request cURL

```

```

#### Response body

```

```

#### Response headers

```

```

### /app/user/login/ (POST)

_Not yet implemented_

#### Request cURL

```

```

#### Response body

```

```

#### Response headers

```

```

### /app/user/new/ (POST)

_Not yet implemented_

#### Request cURL

```

```

#### Response body

```

```

#### Response headers

```

```

### /app/user/update/ (PATCH)

_Not yet implemented_

#### Request cURL

```

```

#### Response body

```

```

#### Response headers

```

```

### /app/user/delete/ (DELETE)

_Not yet implemented_

#### Request cURL

```

```

#### Response body

```

```

#### Response headers

```

```
