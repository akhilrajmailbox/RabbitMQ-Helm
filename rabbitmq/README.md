# RabbitMQ Server

RabbitMQ Deployment on K8s

## TL;DR;

```
kubectl create ns rabbitmq
helm repo add ar-repo https://akhilrajmailbox.github.io/rabbitmq-helm/charts
helm install rabbitmq ed-repo/rabbitmq -n rabbitmq
```

The command deploys the RabbitMQ on the Kubernetes cluster in the default configuration. The [Configuration](#configuration) section lists the parameters that can be configured during installation.

### Custom parameters

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```
helm install rabbitmq ed-repo/rabbitmq -n rabbitmq --set service.port=5672
```

Alternatively, a YAML file can be provided while installing the chart. This file specifies values to override those provided in the default `values.yaml`. For example,

```
helm install rabbitmq ed-repo/rabbitmq -n rabbitmq -f my-values.yaml
```

## Updating the chart

To update the chart run:

```
helm upgrade rabbitmq ed-repo/rabbitmq -n rabbitmq -f my-values.yaml
```

## Uninstalling the Chart

To uninstall/delete the `rabbitmq` deployment:

```
helm uninstall rabbitmq -n rabbitmq
```

The command removes all the Kubernetes components associated with the chart and deletes the release.



## Configuration

The following table lists the configurable parameters of the Hyperledger Fabric Orderer chart and default values.

| Parameter                          | Description                                       | Default                                                   |
| ---------------------------------- | ------------------------------------------------- | --------------------------------------------------------- |
| `cluster.enabled`                  | cluster configuration                             | `false`                                                   |
| `cluster.replicaCount`             | number of node if cluster enabled                 | `3`                                                       |
| `rabbitmq.username`                | username                                          | `rabbitmq`                                                |
| `rabbitmq.password`                | password                                          | `MySecurePass`                                            |
| `rabbitmq.erlangCookie`            | erlang cookies                                    | `erlang-cookie=c-is-for-cookie-thats-good-enough-for-me`  |
| `priorityClassName`                | Pod Priority and Preemption                       | `-`                                                       |
| `image.repository`                 | docker repository                                 | `rabbitmq`                                                |
| `image.tag`                        | image tag                                         | `3.8.0-management`                                        |
| `image.pullPolicy`                 | Image pull policy                                 | `Always`                                                  |
| `tls.enabled`                      | tls configuration for rabbitmq                    | `false`                                                   |
| `tls.existingSecret`               | secrets created before the deployment             | `rabbitmq-cert`                                           |
| `service.port`                     | TCP port                                          | `5672`                                                    |
| `service.tlsPort`                  | TCP tls port                                      | `5671`                                                    |
| `service.managementPort`           | TCP management port                               | `15672`                                                   |
| `service.tlsmanagementPort`        | TCP management ssl port                           | `15671`                                                   |
| `service.type`                     | K8S service type exposing ports, e.g. `ClusterIP` | `LoadBalancer`                                            |
| `persistence.enabled`              | persistence volume configuration                  | `true`                                                    |
| `persistence.name`                 | pvc name                                          | `rabbitmq-pvc`                                            |
| `persistence.accessMode`           | Use volume configuration ex:  ReadOnly            | `ReadWriteOnce`                                           |
| `persistence.size`                 | Size of data volume (adjust for production!)      | `10Gi`                                                    |
| `persistence.storageClass`         | Storage class of backing pvc                      | `default`                                                 |
| `podDisruptionBudget.enabled`      | enable or disable podDisruptionBudget             | `false`                                                   |
| `podDisruptionBudget.name`         | podDisruptionBudget name                          | `rabbitmq-pdb`                                            |
| `podDisruptionBudget.minAvailable` | Min Available pod need to up                      | `1`                                                       |
| `podDisruptionBudget.maxUnavailable` | Max Unvailable pod can be to down               | `-`                                                       |
| `networkPolicy.enabled`            | enable or diable networkPolicy                    | `rabbitmq-pdb`                                            |
| `networkPolicy.allowExternal`      | allow external connection (if networkPolicy enabled)| `1`                                                     |
| `networkPolicy.additionalRules`    | extra networkPolicy rules                         | `{}`                                                      |
| `resources`                        | CPU/Memory resource requests/limits              | `{}`                                                       |
| `affinityenabled`                  | enable or disable Affinity                       | `false`                                                    |
| `affinity`                         | Affinity settings for pod assignment             | `{}`                                                       |
| `nodeSelector`                     | Node labels for pod assignment                   | `{}`                                                       |
| `tolerations`                      | Toleration labels for pod assignment             | `[]`                                                       |