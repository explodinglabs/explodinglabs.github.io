---
layout: post
title: "Django Rest Framework: Permissions Cheatsheet"
date: 2017-01-27
permalink: /django/drf-permissions-cheatsheet
comments: true
---

Permission Class                        | Unauthenticated           | Authenticated
-|-
`AllowAny`                              | Full access               | Full access
`IsAuthenticated`                       | No access                 | Full access
`IsAdminUser`                           | No access                 | Only Admin user has access (full access)
`IsAuthenticatedOrReadOnly`             | Read access               | Full access
`DjangoModelPermissions`                | No access                 | Read access; write requires model permissions
`DjangoModelPermissionsOrAnonReadOnly`  | Read access               | Read access; write requires model permissions
`DjangoObjectPermissions`               | Depends on the object     | Depends on the object
Custom Permissions                      | Customize your own        | Customize your own
{:.mbtablestyle}
