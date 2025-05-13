# sqs

## Run
```
docker-compose up -d
```

## Working with queues

### Default queue
To make use of this queue, point your client to: http://localhost:9324/queue/default

### Dead letter queue
The default dead letter queue is called dlq, configured in opt/elasticmq.conf

### Sending a message
To send messages to a queue you need to specify the new endpoint url and queue url along with the message payload. The following example uses the AWS CLI to send a message to the default queue.

```
 aws --endpoint-url http://localhost:9324 sqs send-message --queue-url http://localhost:9324/queue/default --message-body "Hello, queue" --region eu-central-1 --no-sign-request
```
> Notes:
> 
> --region eu-central-1 -> Required based on region config. Default: `eu-central-1`
>
> --no-sign-request -> Required because no need credentials.

Response Success
```
{
    "MD5OfMessageBody": "ed9a32dad42be8901d3a5ad136105170",
    "MessageId": "9f2304b2-b26d-4e5e-a67d-3833b4148d2a"
}
```

### Viewing messages
To view messages, navigate to the web UI (sqs-insight) by pointing your web browser to http://localhost:9325.

You can also poll for messages from the command-line like so:
```
aws --endpoint-url http://localhost:9324 sqs receive-message --queue-url http://localhost:9324/queue/default --wait-time-seconds 10 --region eu-central-1 --no-sign-request 
```

## Creating new queues

You can create new queues by using the command-line or configuring ElasticMQ directly.

### AWS CLI
```
aws --endpoint-url http://localhost:9324 sqs create-queue --queue-name newqueue --region eu-central-1 --no-sign-request
```

### Edit ElasticMQ configuration file

Navigate to the directory where the configuration files reside and edit the elasticmq.conf file to add a new entry for each queue to the queue block.
```
queues {
    default {
        defaultVisibilityTimeout = 10 seconds
        delay = 5 seconds
        receiveMessageWait = 0 seconds
    },
    newqueue {
        defaultVisibilityTimeout = 10 seconds
        delay = 5 seconds
        receiveMessageWait = 0 seconds
    }
}
```

> Note: The configuration directory location inside the container is located at /opt/config. If you mounted that volume onto your host, you can also find the configuration files there.

After editing the elasticmq.conf file, you need to restart the ElasticMQ server by running the supervisorctl restart elasticmq command inside the container. If you're editing the configuration file outside of the container, use this command:

```
docker exec -it alpine-sqs sh -c "supervisorctl restart elasticmq"
```

### Registering new queues with the UI

To be able to visualize newly created queues, you need to edit the sqs-insight.conf file to register the new queue with the UI server. Edits to this file are automatically detected by the server and does not require a restart.

Configure a new endpoint like this:
```
"endpoints": [
        {
           "key": "notValidKey",
           "secretKey": "notValidSecret",
           "region": "eu-central-1",
           "url": "http://localhost:9324/queue/default"
        },
        {
           "key": "notValidKey",
           "secretKey": "notValidSecret",
           "region": "eu-central-1",
           "url": "http://localhost:9324/queue/newqueue"
        }
    ]
```

All the fields, except the url field, are required by sqs-insight to function but are not used when pointing it to a local queue server. This means that the values in those fields are not relevant for the UI to work correctly.

> Consult the AWS CLI Command Reference or the AWS SDK for Java guide for more examples and information.
