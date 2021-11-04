---
layout: post
title: Postgres migrations
permalink: /postgres-migrations
---
Deploy, verify and revert migrations for various common changes.

## Function

Deploy:
```sql
create or replace function api.foo(x int, y text) returns json as $$
declare
begin
    ...
end;
```

Verify:
```sql
assert (select has_function_privilege('api.foo(int, text)', 'execute'));
```

Revert:
```sql
drop function api.foo;
```

## Schema

Deploy:
```sql
create schema api;
```

Verify:
```sql
assert (select * from information_schema.schemata where schema_name = 'api');
```

Revert:
```sql
drop schema api;
```

## Trigger

Deploy:
```sql
create trigger encrypt_pass
before insert or update on auth.user
for each row execute procedure auth.encrypt_pass();
```

Verify:
```sql
assert (select * from information_schema.triggers where trigger_schema = 'auth' and trigger_name = 'encrypt_pass');
```

Revert:
```sql
drop trigger encrypt_pass on auth.user;
```

## View

Deploy:
```sql
create or replace view api.users as select id, email from auth.user;
alter view api.users owner to api_views_owner;
```

Verify:
```sql
assert (select * from information_schema.views where table_schema='api' and viewname='users');
```

Revert:
```sql
drop view api.users;
```
