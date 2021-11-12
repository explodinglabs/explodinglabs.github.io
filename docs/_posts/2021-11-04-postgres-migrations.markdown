---
layout: post
title: Postgres migrations
permalink: /postgres-migrations
---
Deploy, verify and revert migrations for various common changes.

## Extension

Deploy:
```sql
create extension if not exists "foo";
```

Verify:
```sql
assert (select exists (select 1 from pg_extension where extname='foo'));
```

Revert:
```sql
drop extension "foo";
```

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
assert (
    select exists (
        select 1 from information_schema.routines
        where specific_schema = 'api'
        and routine_name = 'foo'
    )
);
```

Revert:
```sql
drop function api.foo;
```

## Role

Deploy:
```sql
create role foo nologin;
-- or
create role foo noinherit login password 'mysecretpassword';
```

Verify:
```sql
assert (select exists (select 1 from information_schema.enabled_roles where role_name = 'foo'));
```

Revert:
```sql
drop role foo;
```

## Table

Deploy:
```sql
create table if not exists foo.bar (
    id serial primary key,
    created_at timestamp not null default now(),
    updated_at timestamp not null default now(),
    ...
);
```

Verify:
```sql
assert (
    select exists (
        select 1 from information_schema.tables
        where table_schema = 'foo'
        and table_name='bar'
    )
);
```

Revert:
```sql
drop table foo.bar;
```

## Privileges

Deploy:
```sql
grant select on api.users to web_user;
```

Verify:
```sql
-- For a table or view
assert (
    select exists (
        select 1 from information_schema.table_privileges
        where privilege_type = 'SELECT'
        and table_schema='api'
        and table_name = 'users'
        and grantee='web_user'
    )
);

-- For a function
assert (select has_function_privilege('anon', 'api.login(text, text)', 'execute'));
```

Revert:
```sql
revoke select on api.users from web_user;
```

## Schema

Deploy:
```sql
create schema foo;
```

Verify:
```sql
assert (select exists (select 1 from information_schema.schemata where schema_name = 'foo'));
```

Revert:
```sql
drop schema foo;
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
assert (
    select exists (
        select 1 from information_schema.triggers
        where event_object_schema = 'auth'
        and event_object_table = 'user'
        and trigger_name = 'encrypt_pass'
    )
);
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
assert (
    select exists (
        select 1 from information_schema.views
        where table_schema='api'
        and table_name='users'
    )
);
```

Revert:
```sql
drop view api.users;
```
