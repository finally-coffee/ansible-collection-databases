# `finallycoffee.databases.postgresql` ansible role

PostgreSQL is the self proclaimed "world's most advanced" open source relational
database. This ansible role can deploy and configure postgresql.

By default, the role configures the remote's effective ansible user with
peer authentication for the (postgresql) role `postgres` on all databases (with all grants).

## Required configuration

Set `postgresql_superuser_password` to your superusers desired password.

## Optional configuration

Set `postgresql_major_version` to your desired postgresql major version,
for supported major versions see [`defaults/main/main.yml`](defaults/main/main.yml#L6).

This role can be executed multiple times with different
`postgresql_major_version` values to provide new database versions for up-to-
date applications and older versions for software which does not yet support
them. Container name and host mounts encode the major version to prevent
accidental usage of the 'wrong' `PGDATA` directory.

## Requirements

- `psycopg2` (pip) package
- `docker` (pip) package
