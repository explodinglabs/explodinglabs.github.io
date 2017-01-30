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
`AllowAny`                              |           |           |   |
`IsAuthenticated`                       | Forbidden | Forbidden |   |
`IsAdminUser`                           | Forbidden | Forbidden | Staff only |
`IsAuthenticatedOrReadOnly`             |           | Forbidden |   |
`DjangoModelPermissions`                | Forbidden | Forbidden | Requires Model Permissions |
`DjangoModelPermissionsOrAnonReadOnly`  |           | Forbidden | Requires Model Permissions |
`DjangoObjectPermissions`               | Forbidden | Forbidden | Requires Object Permissions |
{:.mbtablestyle}

- *Read access* means `GET`, `OPTIONS` and `HEAD`.
- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
