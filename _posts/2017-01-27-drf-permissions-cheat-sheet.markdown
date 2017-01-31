---
layout: post
title: "Django Rest Framework: Permissions Cheatsheet"
date: 2017-01-27
permalink: /django/drf-permissions-cheatsheet
comments: true
---

A guide to DRF's built-in permission classes.

Permission Class                        | Unauthenticated Read | Unauthenticated Write | Authenticated
-|-
`AllowAny`                              |           |           | 
`IsAuthenticatedOrReadOnly`             |           | Forbidden | 
`IsAuthenticated`                       | Forbidden | Forbidden | 
`DjangoModelPermissionsOrAnonReadOnly`  |           | Forbidden | Requires Model Permissions
`DjangoModelPermissions`                | Forbidden | Forbidden | Requires Model Permissions
`DjangoObjectPermissions`               | Forbidden | Forbidden | Requires Object Permissions
`IsAdminUser`                           | Forbidden | Forbidden | Requires is_staff=True
{:.mbtablestyle}

- *Read access* means `GET`, `OPTIONS` and `HEAD`.
- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
