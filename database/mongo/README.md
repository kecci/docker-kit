# Docker Mongo Local

Run Docker-compose:
```
$ docker-compose up -d
```

Run:
```
$ docker run --name mongo-container -e MONGO_INITDB_DATABASE=local -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=123456 -p 27017-27019:27017-27019 -d mongo
```