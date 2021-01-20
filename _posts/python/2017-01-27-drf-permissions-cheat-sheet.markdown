---
layout: post
category: python
title: Django REST Framework - Permissions Matrix
permalink: /python/drf-permissions-cheatsheet
redirect_from:
    - /django/drf-permissions-cheatsheet
    - /django/drf-permissions-matrix
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
