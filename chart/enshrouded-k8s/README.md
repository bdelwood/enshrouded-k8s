# enshrouded-k8s

![Version: 0.7.0](https://img.shields.io/badge/Version-0.7.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.5.0](https://img.shields.io/badge/AppVersion-1.5.0-informational?style=flat-square)

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
| gameServer.difficulty | string | `"Default"` | Server difficulty.  Preset can be `Default \| Relaxed \| Hard \| Survival \| Custom`. Must be `Custom` to set individual server difficulty settings. Use `extraEnv` and prepend with `SERVER_GS_`. See container image [docs](https://github.com/mornedhels/enshrouded-server/blob/main/docs/SERVER_DIFFICULTY.md) for more info. |
| gameServer.existingSecret | string | `""` | Name of an existing secret for the server password. |
| gameServer.gameBranch | string | `"public"` | Which Steam branch to use for the game server. |
| gameServer.logDir | string | `"./logs"` | Directory for logs sets logDirectory in game server config   |
| gameServer.password | string | `""` | Server password If one is not provided or an existing secret it not provided, one will be generated. |
| gameServer.players | int | `16` | Number of players allowed on the server concurrently. |
| gameServer.roles | list | `[]` | A list of roles for the game server. Each role includes a name, an optional password, a list of permissions, and the number of reserved slots. If the password is empty or missing, one will be generated. The role passwords can be provided with an existing secret via `existingSecret`, where the key must have the format `<role-name>-password`. See the [official docs](https://enshrouded.zendesk.com/hc/en-us/articles/19191581489309-Server-Roles-Configuration) for more details on roles. |
| gameServer.saveDir | string | `"./savegame"` | Directory for game saves sets saveDirectory in game server config |
| gameServer.serverIP | string | `"0.0.0.0"` | Server IP used Enshrouded server settings |
| gameServer.serverName | string | `""` | Custom server name. |
| gameServer.service.nodePort | int | `nil` | Node port for the game server (for NodePort service type). |
| gameServer.service.port | int | `15637` | Service port for the game server. |
| gameServer.steamcmdArgs | string | `"validate"` | Extra arguments to pass to steamcmd when updating. |
| gameServer.update.check_players | bool | `false` | Check if players are connected before updating.  |
| gameServer.update.cron_expression | string | `"*/30 * * * *"` | Cron expression for updates. Defines when the update check should run. The default value checks for updates every half hour. Use standard cron format. |
| hooks.backup.post | string | `""` | Command to run after backup & cleanup |
| hooks.backup.pre | string | `""` | Command to run before backup & cleanup |
| hooks.bootstrap | string | `""` | Command to run after general bootstrap |
| hooks.update.post | string | `""` | Command to run after update |
| hooks.update.pre | string | `""` | Command to run before update |
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
| probes | object | `{"liveness":{},"readiness":{}}` | Liveness and readiness probes. |
| probes.liveness | object | `{}` | Liveness probe |
| probes.readiness | object | `{}` | Readiness probe. |
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
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
