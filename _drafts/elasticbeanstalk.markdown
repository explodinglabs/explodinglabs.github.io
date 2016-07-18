---
layout: page
title: "Create an Elastic Beanstalk application with a Docker image"
permalink: /aws/elasticbeanstalk
---
{::options syntax_highlighter_opts="default_lang: shell" /}

<div style="float: right" markdown="1">
![aws](/assets/aws.png)
</div>

Elastic Beanstalk is a service for deploying and scaling web applications. Here
we'll put a Docker application online.

Create an Application on AWS
============================

Create an application
---------------------

    $ aws elasticbeanstalk create-application --application-name web-app

List applications
-----------------

    $ aws elasticbeanstalk describe-applications
    {
        "Applications": [
            {
                "DateUpdated": "2016-07-16T10:13:49.751Z",
                "ApplicationName": "web-app",
                "ConfigurationTemplates": [],
                "DateCreated": "2016-07-16T10:13:49.751Z"
            }
        ]
    }

Delete the Application from AWS
===============================

    $ aws elasticbeanstalk delete-application --application-name web-app
