---
layout: post
title: "ECS Container Instances"
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

Launch a Container Instance
===========================

IAM roles & policies
--------------------

Save these files: [ecs-policy.json](/files/ecs-policy.json) and
[role-policy.json](/files/role-policy.json).

Create role with policy:

    $ aws iam create-role --role-name ecsRole --assume-role-policy-document file://ecs-policy.json
    $ aws iam put-role-policy --role-name ecsRole --policy-name ecsRolePolicy --policy-document file://role-policy.json

Create instance profile with role:

    $ aws iam create-instance-profile --instance-profile-name webserver
    $ aws iam add-role-to-instance-profile --instance-profile-name webserver --role-name ecsRole

Security groups
---------------

    $ aws ec2 create-security-group --group-name MySecurityGroup --description "My security group"

*Note the security group id, which is needed when launching an EC2 instance.*

Open ports 22 and 80:

    $ aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 22 --cidr 0.0.0.0/0
    $ aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 80 --cidr 0.0.0.0/0

Launch an instance
------------------

Launch an EC2 instance in an ECS cluster.

Create an ECS cluster:

    $ aws ecs create-cluster --cluster-name my-cluster

Create a `userdata.txt` (this gets run when the instance is created):

    #!/bin/bash
    echo 'ECS_CLUSTER=my-cluster' >> /etc/ecs/ecs.config

Launch an instance inside the cluster:

    $ aws ec2 run-instances --image-id ami-0bf2da68 --count 1 --instance-type t2.micro --key-name aws-beau-sydney --iam-instance-profile Name= webserver --security-group-id sg-xxxxxx --associate-public-ip-address --user-data file://userdata.txt

Now you can run [tasks and services](/aws/ecs/2016/07/14/ecs-service.html).

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

List tasks
----------



Services
========

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
-------------

    $ aws ecs list-services --cluster my-cluster

Delete a service
----------------

(You'll need to stop the tasks first)

    $ aws ecs delete-service --cluster my-cluster --service web-app
