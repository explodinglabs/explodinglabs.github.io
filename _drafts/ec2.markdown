---
layout: post
title: "Launch an EC2 Instance"
date: 2016-07-17
permalink: /aws/ec2
---
{::options syntax_highlighter_opts="default_lang: shell" /}

<div style="float: right" markdown="1">
![aws](/assets/aws.png)
</div>

> Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides
> resizable compute capacity in the cloud. It is designed to make web-scale
> cloud computing easier for developers.

Create an instance
==================

    $ aws ec2 run-instances --image-id ami-0bf2da68 --count 1 --instance-type t2.nano --key-name aws-beau-sydney --iam-instance-profile Name= webserver --security-group-id sg-xxxxxx --associate-public-ip-address --user-data file://userdata.txt
