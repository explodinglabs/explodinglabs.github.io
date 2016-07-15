---
layout: post
title: "EC2 Instances"
categories: aws ecs
---
{::options syntax_highlighter_opts="default_lang: shell" /}

List running Instances
======================

    $ aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId]' --filters Name=instance-state-name,Values=running --output text

Stop an Instance
================

    $ 
