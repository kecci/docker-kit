# Arangodb

## Interface
Web interface: http://localhost:8529

## Using Arangodb Shell
```
docker exec -it arangodb-arangodb-1 arangosh
```

For specific IP Address:
```
arangosh --server.endpoint tcp://192.168.173.13:8530 --server.username foo --server.database test --server.authentication true
```
