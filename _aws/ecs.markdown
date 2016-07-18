---
layout: post
title: "Launch an ECS Container Instance and run a Container"
date: 2016-07-13
permalink: /aws/ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

<div style="float: right" markdown="1">
![aws](/assets/aws.png)
</div>

Amazon ECS is a highly scalable, fast, container management service that makes
it easy to run, stop, and manage Docker containers on a cluster of EC2
instances.

An ECS Container Instance is an EC2 instance that is running the ECS container
agent, and has been registered into an ECS cluster.

* TOC
{:toc}

Create an Instance Profile
==========================

First we need to create an instance profile for the instance.

And before that, setup the roles for the profile.

Create a role for the profile
-----------------------------

Create two role policy files.

The first I named `ecs-policy.json`:

```json
{
  "Version": "2016-07-13",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

The second I named `role-policy.json`:

```json
{
  "Version": "2016-07-13",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ecr:BatchCheckLayerAvailability",
        "ecr:BatchGetImage",
        "ecr:DescribeRepositories",
        "ecr:GetAuthorizationToken",
        "ecr:GetDownloadUrlForLayer",
        "ecr:GetRepositoryPolicy",
        "ecr:ListImages",
        "ecs:CreateCluster",
        "ecs:DeregisterContainerInstance",
        "ecs:DiscoverPollEndpoint",
        "ecs:Poll",
        "ecs:RegisterContainerInstance",
        "ecs:StartTask",
        "ecs:StartTelemetrySession",
        "ecs:SubmitContainerStateChange",
        "ecs:SubmitTaskStateChange"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

Create a role with the policy:

    aws iam create-role --role-name ecsRole --assume-role-policy-document file://ecs-policy.json
    aws iam put-role-policy --role-name ecsRole --policy-name ecsRolePolicy  --policy-document file://role-policy.json

Create the profile
------------------

Finally, create the instance profile with the new role:

    aws iam create-instance-profile --instance-profile-name webserver
    aws iam add-role-to-instance-profile --instance-profile-name webserver --role-name ecsRole

Launch an EC2 Instance
======================

Create a security group for the Instance
----------------------------------------

Open ports 22 and 80:

    aws ec2 create-security-group --group-name MySecurityGroup
    aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 22 --cidr 0.0.0.0/0
    aws ec2 authorize-security-group-ingress --group-name MySecurityGroup --protocol tcp --port 80 --cidr 0.0.0.0/0

*Note the security group id, which is needed when launching an EC2 instance.*

Launch an instance
------------------

We'll be launching an EC2 instance in an ECS cluster.

Create an ECS cluster:

    aws ecs create-cluster --cluster-name my-cluster

Create a `userdata.txt` (this gets run when the instance is created):

    #!/bin/bash
    echo 'ECS_CLUSTER=my-cluster' >> /etc/ecs/ecs.config

Launch an instance inside the cluster:

    aws ec2 run-instances --count 1 --image-id ami-0bf2da68 --instance-type t2.micro --key-name aws-beau-sydney --iam-instance-profile Name= webserver --security-group-id sg-xxxxxx --associate-public-ip-address --user-data file://userdata.txt

Now you can run tasks and services on the instance.

Start a container
=================

Register a task
---------------

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

Register it:

    aws ecs register-task-definition --cli-input-json file://ecs-task.json

List tasks:

    aws ecs list-tasks --cluster my-cluster

Run the task
------------

    aws ecs run-task --cluster my-cluster --count 1 --task-definition web-app:1

To deregister a task:

    aws ecs deregister-task-definition --task-definition web-app:1

{% comment %}
Services
========

Create a service
----------------

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

    aws ecs create-service --cluster my-cluster --service-name web-app --task-definition web-app:1 --desired-count 2

List services
-------------

    aws ecs list-services --cluster my-cluster

Delete a service
----------------

(You'll need to stop the tasks first)

    aws ecs delete-service --cluster my-cluster --service web-app
{% endcomment %}
