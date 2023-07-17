# Ostara Agent

An [Ostara](https://github.com/krud-dev/ostara) agent is a worker installed in your environment. It plays a pivotal role in connecting Ostara to the services within your environment. By installing an agent, you enable Ostara to discover and monitor your applications automatically.

For more information, visit the [documentation](https://docs.ostara.dev/documentation/agents).

## TL;DR

```console
helm repo add ostara https://krud-dev.github.io/ostara-helm
helm install agent ostara/agent
```

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart, add the Ostara repository and install the chart with the release name `agent`:

```console
helm repo add ostara https://krud-dev.github.io/ostara-helm
helm install agent ostara/agent
```

These commands deploy Ostara Agent on the Kubernetes cluster in the default configuration.

## Uninstalling the Chart

To uninstall/delete the `agent` deployment:

```console
helm delete agent
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Common parameters

| Name                                            | Description                                          | Value                |
| ----------------------------------------------- | ---------------------------------------------------- | -------------------- |
| `replicaCount`                                  | Number of agent replicas to deploy                   | `1`                  |
| `image.repository`                              | Agent image repository                               | `idane/ostara-agent` |
| `image.pullPolicy`                              | Agent image pull policy                              | `Always`             |
| `image.tag`                                     | Agent image tag override                             | `""`                 |
| `imagePullSecrets`                              | Specify docker-registry secret names as an array     | `[]`                 |
| `nameOverride`                                  | String to partially override agent.fullname          | `""`                 |
| `fullnameOverride`                              | String to fully override agent.fullname              | `""`                 |
| `serviceAccount.create`                         | Specifies whether a ServiceAccount should be created | `true`               |
| `serviceAccount.annotations`                    | Annotations to add to the ServiceAccount             | `{}`                 |
| `serviceAccount.name`                           | The name of the ServiceAccount to use.               | `""`                 |
| `podAnnotations`                                | Annotations to add to the agent pods                 | `{}`                 |
| `podSecurityContext`                            | Agent pods' Security Context                         | `{}`                 |
| `securityContext`                               | Agent containers' Security Context                   | `{}`                 |
| `service.type`                                  | Kubernetes Service type                              | `ClusterIP`          |
| `service.port`                                  | Agent service port                                   | `14444`              |
| `ingress.enabled`                               | Enables Ingress                                      | `false`              |
| `ingress.annotations`                           | Ingress annotations                                  | `{}`                 |
| `ingress.hosts`                                 | Ingress accepted hostnames                           | `{}`                 |
| `ingress.tls`                                   | Ingress TLS configuration                            | `[]`                 |
| `ingress.className`                             | Ingress class name                                   | `""`                 |
| `ingress.hosts`                                 | Ingress accepted hostname                            | `{}`                 |
| `resources.limits`                              | CPU/Memory resource limits                           | `{}`                 |
| `resources.requests`                            | CPU/Memory resource requests                         | `{}`                 |
| `autoscaling.enabled`                           | Enable autoscaling for the agent deployment          | `false`              |
| `autoscaling.minReplicas`                       | Minimum number of agent pods to run                  | `1`                  |
| `autoscaling.maxReplicas`                       | Maximum number of agent pods to run                  | `100`                |
| `autoscaling.targetCPUUtilizationPercentage`    | Target CPU utilization percentage                    | `80`                 |
| `autoscaling.targetMemoryUtilizationPercentage` | Target Memory utilization percentage                 | `80`                 |
| `nodeSelector`                                  | Node labels for agent pod assignment                 | `{}`                 |
| `tolerations`                                   | Tolerations for agent pod assignment                 | `[]`                 |
| `affinity`                                      | Affinity for agent pod assignment                    | `{}`                 |

### Agent parameters

| Name     | Description         | Value |
| -------- | ------------------- | ----- |
| `config` | Agent configuration, a combination of agent specific configuration and standard Spring configuration. For more information, refer to the [documentation](https://docs.ostara.dev/documentation/agents). | `{}`  |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install agent \
  --set imagePullPolicy=Always \
    ostara/agent
```

The above command sets the `imagePullPolicy` to `Always`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm install agent -f values.yaml ostara-agent
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### Setting Pod's affinity

This chart allows you to set your custom affinity using the `affinity` parameter. Find more information about Pod's affinity in the [kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

### Ingress

This chart provides support for ingress resources. If you have an ingress controller installed on your cluster, such as [nginx-ingress-controller](https://github.com/bitnami/charts/tree/main/bitnami/nginx-ingress-controller). You can utilize the ingress controller to serve your application.

To enable ingress integration, please set `ingress.enabled` to `true`.
