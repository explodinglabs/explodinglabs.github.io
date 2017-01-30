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
`AllowAny`                              |   |   |   |
`IsAuthenticated`                       | X | X |   |
`IsAdminUser`                           | X | X | X |
`IsAuthenticatedOrReadOnly`             |   | X |   |
`DjangoModelPermissions`                | X | X | Requires Model Permissions |
`DjangoModelPermissionsOrAnonReadOnly`  |   | X | Requires Model Permissions |
`DjangoObjectPermissions`               | X | X | Requires Object Permissions |
{:.mbtablestyle}

- *Read access* means `GET`, `OPTIONS` and `HEAD`.
- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
