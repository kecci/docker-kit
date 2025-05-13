# Redis Insight
url : https://hub.docker.com/r/redis/redisinsight

## About Redis Insight
Redis Insight is an ideal tool for developers who build with any Redis deployments - including Redis Open Source, Redis Stack, Redis Enterprise Software, Redis Enterprise Cloud, and Amazon ElastiCache - and who want to optimize their development process. Redis Insight lets you visually browse and interact with data, take advantage of the advanced command line interface and diagnostic tools, and so much more⁠.

If you enjoy Redis Insight, star our repository⁠ to let us see the value you find in what we do.

## Run Redis Insight on Docker
You can install Redis Insight using one of the options described below.

If you do not want to persist your Redis Insight data:
```
docker run -d --name redisinsight -p 5540:5540 redis/redisinsight:latest
```

If you want to persist your Redis Insight data, first attach the Docker volume to the /data path and then run the following command:
```
docker run -d --name redisinsight -p 5540:5540 redis/redisinsight:latest -v redisinsight:/data
```

If the previous command returns a permission error, ensure that the user with ID = 1000 has the necessary permissions to access the volume provided (redisinsight in the command above).

Next, point your browser to http://localhost:5540.

Redis Insight also provides a health check endpoint at http://localhost:5540/api/health/ to monitor the health of the running container.