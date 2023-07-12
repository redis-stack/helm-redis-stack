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
