---
layout: post
title: "Django Rest Framework: Permissions Cheatsheet"
date: 2017-01-27
permalink: /django/drf-permissions-cheatsheet
comments: true
---

Permission Class                        | Unauthenticated           | Authenticated
-|-
`AllowAny`                              | Full read/write access    | Full read/write access
`IsAuthenticated`                       | No access                 | Full read/write access
`IsAdminUser`                           | No access                 | Only Admin user has access. They have full read/write access.
`IsAuthenticatedOrReadOnly`             | Read access               | Full read/write access
`DjangoModelPermissions`                | No access                 | Read access; write requires model permissions
`DjangoModelPermissionsOrAnonReadOnly`  | Read access               | Read access; write requires model permissions
`DjangoObjectPermissions`               | Depends on the object     | Depends on the object
Custom Permissions                      | Customize your own        | Customize your own
{:.mbtablestyle}

- *Read access* means `GET`, `OPTIONS` and `HEAD`.
- *Write access* means `POST`, `PUT`, `PATCH` and `DELETE`.
