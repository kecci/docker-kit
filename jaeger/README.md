# jaeger

Run Docker-compose:
```
$ docker-compose up -d
```

| Port | Protocol | Component | Function |
| ---- | ----------- | ---------- | --------- |
| 5775 | UDP |	agent |	accept zipkin.thrift over compact thrift protocol (deprecated, used by legacy clients only)
| 6831 | UDP |	agent |	accept jaeger.thrift over compact thrift protocol
| 6832 | UDP |	agent |	accept jaeger.thrift over binary thrift protocol
| 5778	| HTTP |	agent | 	serve configs |
| 16686	| HTTP |	query | 	serve frontend |
| 14268	| HTTP |	collector | 	accept jaeger.thrift directly from clients |
| 14250	| HTTP |	collector | 	accept model.proto |
| 9411	| HTTP |	collector | 	Zipkin compatible endpoint (optional) |

jaeger Collector Endpoint: http://localhost:14268/api/traces

jaeger UI: http://localhost:16686/

hotrod: http://localhost:8082

Source: https://medium.com/faun/how-to-deploy-jaeger-and-elasticsearch-bf326e774cc8
