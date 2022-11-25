# RabbitMQ

- [RabbitMQ](#rabbitmq)
	- [Setting Up Docker Compose](#setting-up-docker-compose)
	- [Source](#source)


RabbitMQ is an open-source message broker that makes communication between services very easy. In particular, RabbitMQ uses a Publish/Subscribe pattern with an Advanced Message Queuing Protocol.

This reduces the load on web app servers and their delivery times because it efficiently delegates resource-intense tasks to third parties with no other tasks.

In this article, we're going to set up RabbitMQ with Docker Compose. Then, we're going to write a message Sender and Receiver using Go. Before we start, make sure you have the following installed:
- Docker
- Docker Compose
- Go

## Setting Up Docker Compose
If you want to make your code more portable and share the same version of RabbitMQ with your developer colleagues, I highly recommend using Docker.

In this case, we're going to use docker-compose to configure the container name, the volumes and networks, and the ports that RabbitMQ will use. Doing so ensures that everything is isolated and easy to modify.

To start, create a folder called rabbitmq-go in your Golang project folder. Then, create a new file with the name docker-compose.yml. Inside that file, add the following:

```
version: "3.2"
services:
  rabbitmq:
    image: rabbitmq:3-management-alpine
    container_name: 'rabbitmq'
    ports:
        - 5672:5672
        - 15672:15672
    volumes:
        - ~/.docker-conf/rabbitmq/data/:/var/lib/rabbitmq/
        - ~/.docker-conf/rabbitmq/log/:/var/log/rabbitmq
    networks:
        - rabbitmq_go_net

networks:
  rabbitmq_go_net:
    driver: bridge
```

Here's what we've just done:

- image: where we tell Docker which image to pull. We're using an Alpine implementation of RabbitMQ with the management plugin. The Alpine distro is the one you'll want to use if you want to save disk space.
- container_name: this represents the container created from the image above.
- ports: the list of ports that will be mapped from the container to the outside world, for interacting with the queue and the web UI.
- volumes: where we map the log and data from the container to our local folder. This allows us to view the files directly in their local folder structure instead of having to connect to the container.
- networks: where we specify the network's name that the container will be using. This helps to separate container network configurations.

Now that we have this all set up, we can check if RabbitMQ is working correctly. Open a terminal, navigate to your rabbitmq-go folder and run docker-compose up.

This command will pull the `rabbitmq:3-management-alpine` image, create the container rabbitmq and start the service and webUI. You should see something like this:


Once you see this, open your browser and head over to http://localhost:15672. You should see the RabbitMQ UI. Use `guest` as username and password.

Congratulations! You've just started RabbitMQ from a Docker image.

## Source
- https://x-team.com/blog/set-up-rabbitmq-with-docker-compose/