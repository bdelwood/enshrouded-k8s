# enshrouded-k8s

![Version: 0.2.1](https://img.shields.io/badge/Version-0.2.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.4.0](https://img.shields.io/badge/AppVersion-0.4.0-informational?style=flat-square)

A basic chart to deploy Enshrouded dedicated servers.

## Source Code

* <https://github.com/bdelwood/enshrouded-k8s>

## Requirements

Kubernetes: `>=1.26.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity rules for pod scheduling. |
| extraEnv | object | `{}` | Define extra environment variables to pass directly to the container. Any env vars which are set by other values will be overridden. |
| fullnameOverride | string | `""` | Override the full name of the chart. Default is a combination of release name and chart name. |
| gameServer.backup.cron_expression | string | `"*/15 * * * *"` | Cron expression for backup scheduling. Defines when the backups should be triggered. The default value schedules a backup every 15 minutes. Use standard cron format. |
| gameServer.backup.directory | string | `"./backup"` | Directory for backups. Supports relative and absolute paths. |
| gameServer.backup.max_count | int | `0` | Number of backups to keep. When set to 0, never delete backups |
| gameServer.community.enabled | bool | `true` | Enable if you want your server to show up as a community server. Exposes the Steam query port. |
| gameServer.community.service.nodePort | int | `nil` | Node port a community server (for NodePort service type). Defaults to Node port for game server + 1 |
| gameServer.community.service.port | int | `nil` | Service port for a community server. Defaults to the server port + 1 |
| gameServer.existingSecret | string | `""` | Name of an existing secret for the server password. |
| gameServer.gameBranch | string | `"public"` | Which Steam branch to use for the game server. |
| gameServer.logDir | string | `"./logs"` | Directory for logs sets logDirectory in game server config   |
| gameServer.password | string | `""` | Server password If one is not provided or an existing secret it not provided, one will be generated. |
| gameServer.players | int | `16` | Number of players allowed on the server concurrently. |
| gameServer.saveDir | string | `"./savegame"` | Directory for game saves sets saveDirectory in game server config |
| gameServer.serverIP | string | `"0.0.0.0"` | Server IP used Enshrouded server settings |
| gameServer.serverName | string | `""` | Custom server name. |
| gameServer.service.nodePort | int | `nil` | Node port for the game server (for NodePort service type). |
| gameServer.service.port | int | `15636` | Service port for the game server. |
| gameServer.steamcmdArgs | string | `"validate"` | Extra arguments to pass to steamcmd when updating. |
| gameServer.update.check_players | bool | `false` | Check if players are connected before updating.  |
| gameServer.update.cron_expression | string | `"*/30 * * * *"` | Cron expression for updates. Defines when the update check should run. The default value checks for updates every half hour. Use standard cron format. |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.registry | string | `"docker.io"` | Container registry for the image. |
| image.repository | string | `"mornedhels/enshrouded-server"` | Image repository |
| image.tag | string | `""` | Overrides the image tag. Default is the chart `${appVersion}-proton`. |
| nameOverride | string | `""` | Override the name of the chart. Default is the chart name. |
| nodeSelector | object | `{}` | Node selector for pod scheduling. |
| persistence.accessMode | string | `"ReadWriteOnce"` | Access mode for the persistent volume. |
| persistence.enabled | bool | `true` | Enable or disable persistence. |
| persistence.existingClaim | string | `""` | Name of an existing persistentVolumeClaim. |
| persistence.preventDelete | bool | `true` | Prevent Helm from deleting the PVC. Some storageClasses (such as the local-path-provisioner installed by default by k3s) have reclaimPolicy: Delete. |
| persistence.size | string | `"30Gi"` | Size of the persistent volume. |
| persistence.storageClassName | string | `""` | Storage class name for the PVC. |
| podAnnotations | object | `{}` | Annotations to add to the pod. |
| podSecurityContext | object | `{}` | Security context for the pod. |
| resources.limits | object | `{"cpu":8,"memory":"24Gi"}` | Resource limits (CPU, Memory) for the server. |
| resources.requests | object | `{"cpu":6,"memory":"16Gi"}` | Resource requests (CPU, Memory) for the server. |
| securityContext | object | `{}` | Security context for the pod containers. |
| service.type | string | `"LoadBalancer"` | Service type (e.g., LoadBalancer, ClusterIP, NodePort) |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account. |
| serviceAccount.create | bool | `false` | Specifies whether a service account should be created. |
| serviceAccount.name | string | `""` | The name of the service account. |
| tolerations | object | `{}` | Tolerations for pod scheduling. |
| tz | string | `"UTC"` | Timezone setting for the server. |
| updateStrategy | object | `{"type":"Recreate"}` | Update strategy for deployments. |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.12.0](https://github.com/norwoodj/helm-docs/releases/v1.12.0)
