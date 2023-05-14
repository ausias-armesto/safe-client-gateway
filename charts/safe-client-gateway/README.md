# Safe Client Gateway Chart

This chart packages the Safe Client Gateway resources. The chart assumes that there is already an existing Redis instance available and connection attribute should be passed in the values of the Helm Chart

## Parameters

### Common parameters

| Name               | Description                                        | Value |
| ------------------ | -------------------------------------------------- | ----- |
| `nameOverride`     | String to partially override common.names.fullname | `""`  |
| `fullnameOverride` | String to fully override common.names.fullname     | `""`  |

### Installation Parameters

| Name                           | Description                                                      | Value                            |
| ------------------------------ | ---------------------------------------------------------------- | -------------------------------- |
| `replicas`                     | Replicas for deployment                                          | `1`                              |
| `strategy`                     | Strategy for deployment                                          | `Recreate`                       |
| `commonLabels`                 | Labels to add to all related objects                             | `{}`                             |
| `commonAnnotations`            | Annotations to to all related objects                            | `{}`                             |
| `nodeSelector`                 | Object containing node selection constraint to deployment        | `{}`                             |
| `resources`                    | Resource specification to deployment                             | `{}`                             |
| `tolerations`                  | Tolerations specifications to deployment                         | `[]`                             |
| `affinity`                     | Affinity specifications to deployment                            | `{}`                             |
| `image.registry`               | Docker registry to deployment                                    | `registry.hub.docker.com`        |
| `image.repository`             | Docker image repository to deployment                            | `safeglobal/safe-config-service` |
| `image.tag`                    | Docker image tag to deployment                                   | `""`                             |
| `image.pullPolicy`             | Pull policy to deployment as deinfed in                          | `IfNotPresent`                   |
| `service.type`                 | service type                                                     | `ClusterIP`                      |
| `service.ports.number`         | service port number                                              | `8000`                           |
| `service.ports.name`           | service port name                                                | `gunicorn`                       |
| `service.sessionAffinity`      | Control where client requests go, to the same pod or round-robin | `None`                           |
| `persistence.storageClassName` | Storage class name for persisting static files                   | `""`                             |
| `persistence.size`             | Size of the persistence volume                                   | `100M`                           |

### Config Service Parameters

| Name                                 | Description                                                                                              | Value                                        |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| `config.secretKey`                   | Config Service Secret Key. You should generate a random string of 50+ characters for this value in prod. | `""`                                         |
| `config.cgw.url`                     | The Client Gateway URL. This is for triggering webhooks to invalidate its cache for example              | `http://gateway.safe.svc.cluster.local:8000` |
| `config.cgw.flushToken`              | Flush Token                                                                                              | `""`                                         |
| `config.refSecretKey`                | Reference to an existing secret containing the following entries: SECRET_KEY, CGW_FLUSH_TOKEN            | `""`                                         |
| `config.pythonDontWriteBytecode`     | pythonDontWriteBytecode                                                                                  | `true`                                       |
| `config.debug`                       | Enable debug                                                                                             | `true`                                       |
| `config.rootLogLevel`                | Log Level                                                                                                | `DEBUG`                                      |
| `config.django.allowedHosts`         | Allowed hosts                                                                                            | `*`                                          |
| `config.postgres.secretReferenceKey` | Reference to an existing secret containing the following entries: username, password                     | `""`                                         |
| `config.postgres.username`           | PostgreSQL user                                                                                          | `""`                                         |
| `config.postgres.password`           | PostgreSQL user's password                                                                               | `""`                                         |
| `config.postgres.database`           | PostgreSQL database name                                                                                 | `safe-config`                                |
| `config.postgres.host`               | PostgreSQL server host                                                                                   | `""`                                         |
| `config.postgres.port`               | PostgreSQL server port                                                                                   | `5432`                                       |
