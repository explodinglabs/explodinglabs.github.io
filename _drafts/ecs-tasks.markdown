---
layout: post
title: "ECS Container Tasks"
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

Tasks
=====

Describe your task in a *Task Definition* file, which I named `ecs-task.json`:

```json
{
  "family": "web-app",
  "containerDefinitions": [
    {
      "image": "project/web-app:latest",
      "name": "web-app",
      "memory": 10,
      "cpu": 10,
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80
        }
      ],
      "essential": true
    }
  ]
}
```

Register the task:

    $ aws ecs register-task-definition --cli-input-json file://ecs-task.json

Run it:

    $ aws ecs run-task --cluster my-cluster --count 1 --task-definition web-app:1
