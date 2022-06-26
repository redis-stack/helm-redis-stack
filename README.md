# Redis-stack helm chart
## Installation

To install the helm chart with latest images, run:

```bash
helm install redis-stack charts/redis-stack --values charts/redis-stack/values.yaml
```

To install the helm chart with specific redis tag, just add ```--set``` tag:

```bash
helm install redis-stack charts/redis-stack --values charts/redis-stack/values.yaml --set statefulset.tag="<TAG>"
```

For example, to run redis stack with redis version 7.0.0, run:

```bash
helm install redis-stack charts/redis-stack --values charts/redis-stack/values.yaml --set statefulset.tag="7.0.0-RC5"
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