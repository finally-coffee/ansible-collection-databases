# `finallycoffee.databases.valkey` ansible role

Valkey is an open source (BSD 3 licensed), high-performance in-memory key/value
data store, ideal for workloads like caching or message queues. It has been
forked from redis 7.2.4 before redis license was changed to SSPL.

Valkey offers compatibility to redis and can be used as a drop-in replacement
for redis.

## Configuration

For the configuration, see the [`redis` role configuration](../redis/README.md#configuration),
and swap the `redis_` prefix of all variables for the `valkey_` prefix.
