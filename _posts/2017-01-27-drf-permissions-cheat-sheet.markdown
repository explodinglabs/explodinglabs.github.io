---
layout: post
title: "Django REST Framework: Permissions Matrix"
date: 2017-01-27
permalink: /django/drf-permissions-matrix
redirect_from: /django/drf-permissions-cheatsheet
comments: true
---
A guide to DRF's built-in permission classes.

Permission Class                        | Unauthenticated Write | Unauthenticated Read | Authenticated
-|-
`AllowAny`                              |           |           |
`IsAuthenticatedOrReadOnly`             | Forbidden |           |
`IsAuthenticated`                       | Forbidden | Forbidden |
`DjangoModelPermissionsOrAnonReadOnly`  | Forbidden |           | Requires Model Permissions
`DjangoModelPermissions`                | Forbidden | Forbidden | Requires Model Permissions
`DjangoObjectPermissions`               | Forbidden | Forbidden | Requires Object Permissions
`IsAdminUser`                           | Forbidden | Forbidden | Admin only
{:.mbtablestyle}

- *Read access* means `GET`, `OPTIONS` and `HEAD`.
- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
