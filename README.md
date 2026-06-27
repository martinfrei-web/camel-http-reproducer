- Install Camel CLI `4.20.0`.

- Start the callee:
```
camel run callee.yaml
```

- Start the caller:

```
camel run caller.yaml \
--property=camel.component.http.skip-control-headers=true \
--property=camel.component.http.skip-request-headers=true \
--property=camel.component.http.skip-response-headers=true
```

Callee console output:

```
2026-06-27 10:07:00.962  INFO 13921 --- [worker-thread-0] callee.yaml:7                            : callee is called with the headers '{Accept-Encoding=gzip, x-gzip, deflate, CamelHttpMethod=POST, CamelHttpPath=/callee, CamelHttpQuery=null, CamelHttpRawQuery=null, CamelHttpUri=/callee, CamelHttpUrl=http://localhost:8080/callee, CamelVertxPlatformHttpLocalAddress=127.0.0.1:8080, CamelVertxPlatformHttpRemoteAddress=127.0.0.1:49498, Connection=keep-alive, Content-Length=23, Host=localhost:8080, User-Agent=Apache-HttpClient/5.5.2 (Java/21.0.11)}' and the body 'Hello Camel from route1'
```

Caller console output:

```
2026-06-27 10:07:01.003  INFO 13968 --- [ - timer://yaml] caller.yaml:17                           : got back the response with the headers '{CamelHttpResponseCode=200, CamelHttpResponseText=OK, foo=bar}' and the body 'Hello Camel from route1'
```

To my understanding we should not see any `CamelXXX` headers by the caller's or callee's logs above, but that's apparently not the case.
