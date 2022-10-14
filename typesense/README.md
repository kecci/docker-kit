# Typesense

![dashboard](assets/dashboard.png)

## Typesense Simple
https://technotrampoline.com/articles/how-to-run-a-local-typesense-server-with-docker-compose/

### Up
```
docker compose up -d
```

### Check
```
curl 'http://localhost:8108/keys' \
    -X GET \
    -H "X-TYPESENSE-API-KEY: local-typesense-api-key"

# Expected response: { "keys": [] }
```

## Typesense With Seeding
https://dev.to/luizhlelis/typesense-search-engine-an-easier-to-use-alternative-to-elasticsearch-33dg

## Typesense Dashboard
https://github.com/bfritscher/typesense-dashboard