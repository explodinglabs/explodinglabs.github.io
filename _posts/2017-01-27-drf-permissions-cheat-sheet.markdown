---
layout: post
title: "Django REST Framework: Permissions Matrix"
date: 2017-01-27
permalink: /django/drf-permissions-matrix
redirect_from: /django/drf-permissions-cheatsheet
---
A guide to DRF's built-in permission classes.

Permission Class                        | Unauthenticated Write | Unauthenticated Read | Authenticated
-|-
`AllowAny`                              |           |           |
`IsAuthenticatedOrReadOnly`             | Forbidden |           |
`IsAuthenticated`                       | Forbidden | Forbidden |
`DjangoModelPermissionsOrAnonReadOnly`  | Forbidden |           | Write requires Model Permissions
`DjangoModelPermissions`                | Forbidden | Forbidden | Write requires Model Permissions
`DjangoObjectPermissions`               | Forbidden | Forbidden | Write requires Object Permissions
`IsAdminUser`                           | Forbidden | Forbidden | Admin only
{:.mbtablestyle}

- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
