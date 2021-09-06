---
layout: post
title: Docker services
permalink: /services
---
Some backend Docker hub services I use.

## Network

```sh
docker network create my_app
```

## Postgres

With default user "postgres".

```sh
docker run -d --name postgres --network my_app --volume $HOME/data/my_app:/var/lib/postgresql/data postgres:12.2
```

## Rabbitmq

```sh
docker run -d --name rabbitmq --network my_app --publish 15672:15672 -e RABBITMQ_SERVER_ADDITIONAL_ERL_ARGS="-rabbit channel_max 0" rabbitmq:3
```

The open port is for the web admin, so queues can be created. (This should be
done in a better way.)

Enable the "rabbitmq_management" plugin.
```sh
docker exec rabbitmq rabbitmq-plugins enable rabbitmq_management
```

After a few seconds, visit
[http://localhost:15672/#/queues](http://localhost:15672/#/queues) and login as
guest:guest to create a queue.


(Will need to be restarted to add channel bridges - separate them with commas.)

## ssehub

Create an `ssehub.json`:
```
{
  "server": {
    "enablePost": false,
    "port": 8080,
    "bind-ip": "0.0.0.0",
    "logdir": "./",
    "pingInterval": 5,
    "pingEvent": false,
    "threadsPerChannel": 2,
    "allowUndefinedChannels": true
  },
  "amqp": {
    "enabled": true,
    "host": "rabbitmq",
    "port": 5672,
    "user": "guest",
    "password": "guest",
    "exchange": "amq.fanout"
  },
  "default": {
    "cacheAdapter": "leveldb",
    "cacheLength": 500,
    "allowedOrigins": "*",
    "restrictPublish": ["127.0.0.1"]
  }
}
```

```sh
docker run -d --name ssehub --network my_app --publish 6000:8080 --volume $PWD/ssehub.json:/ssehub/conf/config.json quay.io/vgno/ssehub:v0.2.2
```
