---
layout: post
title: "ECS Container Services"
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

Create a Service
================

Define your service in a *Service Definition* file, which I named `ecs-service.json`:

```json
{
    "cluster": "my-cluster",
    "serviceName": "web-app",
    "taskDefinition": "web-app:13",
    "desiredCount": 1,
    "role": "ecsRole"
}
```

Create the service:

    $ aws ecs create-service --cluster my-cluster --service-name web-app --task-definition web-app:1 --desired-count 2

List services
=============

    $ aws ecs list-services --cluster my-cluster

Delete a service
================

(You'll need to stop the tasks first)

    $ aws ecs delete-service --cluster my-cluster --service web-app
