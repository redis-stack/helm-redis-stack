[![Helm Chart](https://img.shields.io/github/v/release/redis-stack/helm-redis-stack.svg)](https://github.com/redis-stack/helm-redis-stack/releases/latest)
[![redis-stack docker pulls](https://img.shields.io/docker/pulls/redis/redis-stack?label=redis-stack)](https://img.shields.io/docker/pulls/redis/redis-stack)
[![redis-stack-server docker pulls](https://img.shields.io/docker/pulls/redis/redis-stack-server?label=redis-stack-server)](https://img.shields.io/docker/pulls/redis/redis-stack-server)

# Redis-stack helm chart
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

## Production resource tuning

When deploying the production-ready `redis-stack-server` chart, pinning CPU/memory requests and limits is critical so your scheduler can reserve the right capacity. The chart exposes the `redis_stack_server.resources` block in `charts/redis-stack-server/values.yaml`:

```yaml
redis_stack_server:
  resources:
    requests:
      cpu: 100m
      memory: 1Gi
    limits:
      cpu: 500m
      memory: 2Gi
```

Adjust these values for your node sizes (e.g. `cpu: 250m` requests and `cpu: 1` limit with proportional memory) either by editing the values file or overriding via `--set redis_stack_server.resources.requests.memory=...`. Apply the tuned profile with something like `helm upgrade --install redis-stack redis-stack/redis-stack-server -f values-production.yaml`.

Verify the pod receives the requests/limits you expect using `kubectl describe pod <name>` before pushing to production.
