---
layout: page
title: "Create ECS Container Services"
date: 2016-07-14 14:52:56 +10:00
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

Services
========

Create a service:

    $ aws ecs create-service --cluster MyCluster --service-name web-app --task-definition web-app:1 --desired-count 2

Delete the service (stop the tasks first):

    $ aws ecs delete-service --cluster looked --service web-app
