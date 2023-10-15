[![Helm Chart](https://img.shields.io/github/v/release/redis-stack/helm-redis-stack.svg)](https://github.com/redis-stack/helm-redis-stack/releases/latest)
[![redis-stack docker pulls](https://img.shields.io/docker/pulls/redis/redis-stack?label=redis-stack)](https://img.shields.io/docker/pulls/redis/redis-stack)
[![redis-stack-server docker pulls](https://img.shields.io/docker/pulls/redis/redis-stack-server?label=redis-stack-server)](https://img.shields.io/docker/pulls/redis/redis-stack-server)

# Redis-stack helm chart

## How do I Redis?

[Learn for free at Redis University](https://university.redis.com/)

[Build faster with the Redis Launchpad](https://launchpad.redis.com/)

[Try the Redis Cloud](https://redis.com/try-free/)

[Dive in developer tutorials](https://developer.redis.com/)

[Join the Redis community](https://redis.com/community/)

[Work at Redis](https://redis.com/company/careers/jobs/)

## Installation

To add the repo:

```bash
helm repo add redis-stack https://redis-stack.github.io/helm-redis-stack/
```

To install redis-stack helm chart with latest images, run:

```bash
helm install redis-stack redis-stack/redis-stack
```

To install redis-stack-server helm chart with latest images, run:

```bash
helm install redis-stack redis-stack/redis-stack-server
```

To install the helm chart with specific redis tag, just add ```--set``` tag:

```bash
helm install redis-stack redis-stack/redis-stack --set redis_stack.tag="<TAG>"
```

For example, to run redis stack with redis version 7.0.0, run:

```bash
helm install redis-stack redis-stack/redis-stack --set redis_stack.tag="7.0.0-RC5"
```


## Usage

To connect to redis-cli run:

```bash
kubectl get pods -o name | grep redis-stack
```

Copy the name of the pod (E.g. redis-stack-77d596476d-6j4d2) and run the following command:

```bash
kubectl exec -it <POD_NAME> -- redis-cli
```

By default redis-stack will have no password, Redis Stack supports the ability to configure multiple named users, each with their own password and access control configuration.  Refer to the [Redis Access Control List documentation](https://redis.io/docs/management/security/acl/) for more information. Alternatively the configuration file can be modified and the *requirepass* directive added. This can also be triggered via the *REDIS_ARGS* environment variable. Examples are available on the [docker image page](https://hub.docker.com/repository/docker/redis/redis-stack-server/)
