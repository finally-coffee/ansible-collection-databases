# `finallycoffee.databases.redis` ansible role

Redis is the self-proclaimed world's fastest data platform for caching,
vector search and NoSQL databases. Since version 7.2.4, it is no longer
considered "Free and open source software" (FOSS), with redis switching
their license to the "Serverside public license" (SSPL).

Setting the `redis_version` to higher than `7.2.4` means you will deploy
the SSPL-licensed version to redis.

## Configuration

All container-related options to the `docker_container` ansible module
are available under the `redis_container_*` namespace, for example use
`redis_container_ports: [ '127.0.0.1:6379:6370/tcp' ]` to map the
containers port 6379 to the docker host.

Redis-related config options are either available in the `redis_config_*`
namespace or can be specified by setting them as a dictionary in
`redis_config`

### Authentication and authorization

Redis ACL can be specified as an array in the `redis_config_user` variable
 - see [the redis documentation](https://github.com/redis/redis/blob/unstable/redis.conf#L869)
for the format. Per default, the `default` user is able to connect without
any password. To require a password and use a different user, override
the variable, for example `redis_config_user: [ 'username on +@all -DEBUG ~* >secret' ]`.

## Redis on a unix socket

To make redis available on a unix socket, a directory must be supplied in which the
socket lives:
```yaml
redis_container_socket: /var/run/redis.sock
redis_container_volumes:
  - "/path/to/socket/on/host/redis.sock:{{ redis_container_socket }}:z"
redis_config_unixsocket: "{{ redis_container_socket }}"
```

## Container specific information

Redis publishes their official container image in both a debian-based and an
alpine-based variant. Which image should be used can be configured in
`redis_container_image_flavour`, which defaults to `alpine`, which is smaller
in size but also includes less related / debugging tools. To use the debian-
based image, unset the flavour using `redis_container_image_flavour: ~`.
