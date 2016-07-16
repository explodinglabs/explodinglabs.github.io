---
layout: page
title: "Create an ECR Container Repository and push a Docker image"
permalink: /aws/ecr
---
{::options syntax_highlighter_opts="default_lang: shell" /}

<div style="float: right" markdown="1">
![aws](/assets/aws.png)
</div>

ECR is a Docker container registry that makes it easy for developers to store,
manage, and deploy Docker container images.

<div class="note">
    <h5>Important</h5>
    Not all AWS regions support ECR. If like me, your default region is not
    supported, remember to specify the region whenever using ECR commands (e.g.
    aws ecr --region us-west-2).
</div>

Repositories
============

Create repository
-----------------

    aws ecr create-repository --repository-name project/web-app

Delete repository
-----------------

    aws ecr delete-repository --repository-name project/web-app

Images
======

Login
-----

Docker needs to be logged into the registry. The aws client can output the
required docker command to login with.

    aws ecr get-login

Paste the output to login.

Push an image
-------------

First tag it with your ECR repository address:

    docker tag myimage aws_account_id.dkr.ecr.us-west-2.amazonaws.com/project/web-app

Then push it:

    docker push aws_account_id.dkr.ecr.us-west-2.amazonaws.com/project/web-app

List images
-----------

    aws ecr list-images --repository-name project/web-app

Delete an image
---------------

    aws ecr batch-delete-image --repository-name project/web-app --image-ids imageTag=latest
