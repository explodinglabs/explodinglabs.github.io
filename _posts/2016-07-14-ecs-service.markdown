---
layout: post
title: "Create an ECS service"
date: 2016-07-14 14:52:56 +10:00
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

Register a task
===============

    $ aws ecs register-task-definition --cli-input-json file://ecs-task.json
    $ aws ecs run-task --cluster MyCluster --count 1 --task-definition web-app:1

Generate a Service Definition
=============================

    $ aws ecs create-service --generate-cli-skeleton |tee ecs-service.json
