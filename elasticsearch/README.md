# Elasticsearch

Source: https://github.com/davidbkemp/advanced-elasticsearch-training

Start
```
docker-compose up -d
```

Elasticsearch should now be available on http://localhost:9200

![Image](assets/elasticsearch-health.png)

Kibana should now be available on http://localhost:5601 or http://localhost:25601

Down
```
docker-compose down 
```

Delete Volume
```
docker-compose down -v
```