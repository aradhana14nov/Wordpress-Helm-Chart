# Configuration Parameters of WordPress Helm Chart

The following table lists the configurable parameters of the WordPress chart and their default values per section/component:

### Global parameters

```

| Parameter                 | Description                                     | Default                                                 |
|---------------------------|-------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`    | Global Docker image registry                    | `nil`                                                   |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`     | Global storage class for dynamic provisioning   | `nil`                                                   |

```

### Common parameters

```

| Parameter                 | Description                                     | Default                                                 |
|---------------------------|-------------------------------------------------|---------------------------------------------------------|
| `nameOverride`            | String to partially override wordpress.fullname | `nil`                                                   |
| `fullnameOverride`        | String to fully override wordpress.fullname     | `nil`                                                   |
| `clusterDomain`           | Default Kubernetes cluster domain               | `cluster.local`                                         |

```

### WordPress parameters


```

| Parameter                            | Description                                                                   | Default                                                 |
|--------------------------------------|-------------------------------------------------------------------------------|---------------------------------------------------------|
| `image.registry`                     | WordPress image registry                                                      | `docker.io`                                             |
| `image.repository`                   | WordPress image name                                                          | `bitnami/wordpress`                                     |
| `image.tag`                          | WordPress image tag                                                           | `{TAG_NAME}`                                            |
| `image.pullPolicy`                   | WordPress image pull policy                                                   | `IfNotPresent`                                          |
| `image.pullSecrets`                  | Specify docker-registry secret names as an array                              | `[]` (does not add image pull secrets to deployed pods) |
| `image.debug`                        | Specify if debug logs should be enabled                                       | `false`                                                 |
| `wordpressSkipInstall`               | Skip wizard installation                                                      | `false`                                                 |
| `wordpressUsername`                  | User of the application                                                       | `user`                                                  |
| `wordpressPassword`                  | Application password                                                          | _random 10 character long alphanumeric string_          |
| `wordpressEmail`                     | Admin email                                                                   | `user@example.com`                                      |
| `wordpressFirstName`                 | First name                                                                    | `FirstName`                                             |
| `wordpressLastName`                  | Last name                                                                     | `LastName`                                              |
| `wordpressBlogName`                  | Blog name                                                                     | `User's Blog!`                                          |
| `wordpressTablePrefix`               | Table prefix                                                                  | `wp_`                                                   |
| `wordpressScheme`                    | Scheme to generate application URLs [`http`, `https`]                         | `http`                                                  |
| `allowEmptyPassword`                 | Allow DB blank passwords                                                      | `true`                                                  |
| `allowOverrideNone`                  | Set Apache AllowOverride directive to None                                    | `false`                                                 |
| `customHTAccessCM`                   | Configmap with custom wordpress-htaccess.conf directives                      | `nil`                                                   |
| `smtpHost`                           | SMTP host                                                                     | `nil`                                                   |
| `smtpPort`                           | SMTP port                                                                     | `nil`                                                   |
| `smtpUser`                           | SMTP user                                                                     | `nil`                                                   |
| `smtpPassword`                       | SMTP password                                                                 | `nil`                                                   |
| `smtpUsername`                       | User name for SMTP emails                                                     | `nil`                                                   |
| `smtpProtocol`                       | SMTP protocol [`tls`, `ssl`, `none`]                                          | `nil`                                                   |
| `extraEnv`                           | Additional container environment variables                                    | `[]`                                                    |
| `extraVolumeMounts`                  | Additional volume mounts                                                      | `[]`                                                    |
| `extraVolumes`                       | Additional volumes                                                            | `[]`                                                    |
| `sidecars`                           | Attach additional sidecar containers to the pod                               | `nil`                                                   |
| `replicaCount`                       | Number of WordPress Pods to run                                               | `1`                                                     |
| `updateStrategy`                     | Set up update strategy                                                        | `RollingUpdate`                                         |
| `schedulerName`                      | Name of the alternate scheduler                                               | `nil`                                                   |
| `securityContext.enabled`            | Enable security context for WordPress pods                                    | `true`                                                  |
| `securityContext.fsGroup`            | Group ID for the WordPress filesystem                                         | `1001`                                                  |
| `securityContext.runAsUser`          | User ID for the WordPress container                                           | `1001`                                                  |
| `resources.limits`                   | The resources limits for the WordPress container                              | `{}`                                                    |
| `resources.requests`                 | The requested resources for the WordPress container                           | `{"memory": "512Mi", "cpu": "300m"}`                    |
| `nodeSelector`                       | Node labels for pod assignment                                                | `{}` (evaluated as a template)                          |
| `tolerations`                        | Tolerations for pod assignment                                                | `[]` (evaluated as a template)                          |
| `affinity`                           | Affinity for pod assignment                                                   | `{}` (evaluated as a template)                          |
| `podAnnotations`                     | Pod annotations                                                               | `{}` (evaluated as a template)                          |
| `healthcheckHttps`                   | Use https for liveliness and readiness                                        | `false`                                                 |
| `livenessProbe.enabled`              | Enable/disable livenessProbe                                                  | `true`                                                  |
| `livenessProbe.initialDelaySeconds`  | Delay before liveness probe is initiated                                      | `120`                                                   |
| `livenessProbe.periodSeconds`        | How often to perform the probe                                                | `10`                                                    |
| `livenessProbe.timeoutSeconds`       | When the probe times out                                                      | `5`                                                     |
| `livenessProbe.failureThreshold`     | Minimum consecutive failures for the probe                                    | `6`                                                     |
| `livenessProbe.successThreshold`     | Minimum consecutive successes for the probe                                   | `1`                                                     |
| `livenessProbeHeaders`               | Headers to use for livenessProbe                                              | `{}`                                                    |
| `readinessProbe.enabled`             | Enable/disable readinessProbe                                                 | `true`                                                  |
| `readinessProbe.initialDelaySeconds` | Delay before readiness probe is initiated                                     | `30`                                                    |
| `readinessProbe.periodSeconds`       | How often to perform the probe                                                | `10`                                                    |
| `readinessProbe.timeoutSeconds`      | When the probe times out                                                      | `5`                                                     |
| `readinessProbe.failureThreshold`    | Minimum consecutive failures for the probe                                    | `6`                                                     |
| `readinessProbe.successThreshold`    | Minimum consecutive successes for the probe                                   | `1`                                                     |
| `readinessProbeHeaders`              | Headers to use for readinessProbe                                             | `{}`                                                    |
| `service.annotations`                | Service annotations                                                           | `{}` (evaluated as a template)                          |
| `service.type`                       | Kubernetes Service type                                                       | `LoadBalancer`                                          |
| `service.port`                       | Service HTTP port                                                             | `80`                                                    |
| `service.httpsPort`                  | Service HTTPS port                                                            | `443`                                                   |
| `service.httpsTargetPort`            | Service Target HTTPS port                                                     | `https`                                                 |
| `service.loadBalancerSourceRanges`   | Restricts access for LoadBalancer (only with `service.type: LoadBalancer`)    | `[]`                                                    |
| `service.metricsPort`                | Service Metrics port                                                          | `9117`                                                  |
| `service.externalTrafficPolicy`      | Enable client source IP preservation                                          | `Cluster`                                               |
| `service.nodePorts.http`             | Kubernetes http node port                                                     | `""`                                                    |
| `service.nodePorts.https`            | Kubernetes https node port                                                    | `""`                                                    |
| `service.nodePorts.metrics`          | Kubernetes metrics node port                                                  | `""`                                                    |
| `service.extraPorts`                 | Extra ports to expose in the service (normally used with the `sidecar` value) | `nil`                                                   |
| `persistence.enabled`                | Enable persistence using PVC                                                  | `true`                                                  |
| `persistence.existingClaim`          | Enable persistence using an existing PVC                                      | `nil`                                                   |
| `persistence.storageClass`           | PVC Storage Class                                                             | `nil` (uses alpha storage class annotation)             |
| `persistence.accessMode`             | PVC Access Mode                                                               | `ReadWriteOnce`                                         |
| `persistence.size`                   | PVC Storage Request                                                           | `10Gi`                                                  |
```

### Ingress parameters

```

| Parameter                         | Description                                              | Default                        |
|-----------------------------------|----------------------------------------------------------|--------------------------------|
| `ingress.enabled`                 | Enable ingress controller resource                       | `false`                        |
| `ingress.certManager`             | Add annotations for cert-manager                         | `false`                        |
| `ingress.hostname`                | Default host for the ingress resource                    | `wordpress.local`              |
| `ingress.annotations`             | Ingress annotations                                      | `[]` (evaluated as a template) |
| `ingress.extraHosts[0].name`      | Additional hostnames to be covered                       | `nil`                          |
| `ingress.extraHosts[0].path`      | Additional hostnames to be covered                       | `nil`                          |
| `ingress.extraTls[0].hosts[0]`    | TLS configuration for additional hostnames to be covered | `nil`                          |
| `ingress.extraTls[0].secretName`  | TLS configuration for additional hostnames to be covered | `nil`                          |
| `ingress.secrets[0].name`         | TLS Secret Name                                          | `nil`                          |
| `ingress.secrets[0].certificate`  | TLS Secret Certificate                                   | `nil`                          |
| `ingress.secrets[0].key`          | TLS Secret Key                                           | `nil`                          |

```

### Database parameters

```

| Parameter                                | Description                             | Default                                        |
|------------------------------------------|-----------------------------------------|------------------------------------------------|
| `mariadb.enabled`                        | Deploy MariaDB container(s)             | `true`                                         |
| `mariadb.rootUser.password`              | MariaDB admin password                  | `nil`                                          |
| `mariadb.db.name`                        | Database name to create                 | `bitnami_wordpress`                            |
| `mariadb.db.user`                        | Database user to create                 | `bn_wordpress`                                 |
| `mariadb.db.password`                    | Password for the database               | _random 10 character long alphanumeric string_ |
| `mariadb.replication.enabled`            | MariaDB replication enabled             | `false`                                        |
| `mariadb.master.persistence.enabled`     | Enable database persistence using PVC   | `true`                                         |
| `mariadb.master.persistence.accessModes` | Database Persistent Volume Access Modes | `[ReadWriteOnce]`                              |
| `mariadb.master.persistence.size`        | Database Persistent Volume Size         | `8Gi`                                          |
| `externalDatabase.host`                  | Host of the external database           | `localhost`                                    |
| `externalDatabase.user`                  | Existing username in the external db    | `bn_wordpress`                                 |
| `externalDatabase.password`              | Password for the above username         | `nil`                                          |
| `externalDatabase.database`              | Name of the existing database           | `bitnami_wordpress`                            |
| `externalDatabase.port`                  | Database port number                    | `3306`                                         |

```

### Metrics parameters


```

| Parameter                                 | Description                                                                  | Default                                                      |
|-------------------------------------------|------------------------------------------------------------------------------|--------------------------------------------------------------|
| `metrics.enabled`                         | Start a side-car prometheus exporter                                         | `false`                                                      |
| `metrics.image.registry`                  | Apache exporter image registry                                               | `docker.io`                                                  |
| `metrics.image.repository`                | Apache exporter image name                                                   | `bitnami/apache-exporter`                                    |
| `metrics.image.tag`                       | Apache exporter image tag                                                    | `{TAG_NAME}`                                                 |
| `metrics.image.pullPolicy`                | Image pull policy                                                            | `IfNotPresent`                                               |
| `metrics.image.pullSecrets`               | Specify docker-registry secret names as an array                             | `[]` (does not add image pull secrets to deployed pods)      |
| `metrics.podAnnotations`                  | Additional annotations for Metrics exporter pod                              | `{prometheus.io/scrape: "true", prometheus.io/port: "9117"}` |
| `metrics.resources.limits`                | The resources limits for the metrics exporter container                      | `{}`                                                         |
| `metrics.resources.requests`              | The requested resources for the metrics exporter container                   | `{}`                                                         |
| `metrics.serviceMonitor.enabled`          | Create ServiceMonitor Resource for scraping metrics using PrometheusOperator | `false`                                                      |
| `metrics.serviceMonitor.namespace`        | Namespace where servicemonitor resource should be created                    | `nil`                                                        |
| `metrics.serviceMonitor.interval`         | Specify the interval at which metrics should be scraped                      | `30s`                                                        |
| `metrics.serviceMonitor.scrapeTimeout`    | Specify the timeout after which the scrape is ended                          | `nil`                                                        |
| `metrics.serviceMonitor.relabellings`     | Specify Metric Relabellings to add to the scrape endpoint                    | `nil`                                                        |
| `metrics.serviceMonitor.honorLabels`      | honorLabels chooses the metric's labels on collisions with target labels.    | `false`                                                      |
| `metrics.serviceMonitor.additionalLabels` | Used to pass Labels that are required by the Installed Prometheus Operator   | `{}`                                                         |

```

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install my-release \
  --set wordpressUsername=admin \
  --set wordpressPassword=password \
  --set mariadb.mariadbRootPassword=secretpassword \
    stable/wordpress
```

The above command sets the WordPress administrator account username and password to `admin` and `password` respectively. Additionally, it sets the MariaDB `root` user password to `secretpassword`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml stable/wordpress
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

## [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Production configuration

This chart includes a `values-production.yaml` file where you can find some parameters oriented to production configuration in comparison to the regular `values.yaml`. You can use this file instead of the default one.

- Set Apache AllowOverride directive to None:

```diff
- allowOverrideNone: false
+ allowOverrideNone: true
```

- Number of WordPress Pods to run:

```diff
- replicaCount: 1
+ replicaCount: 3
```

- Enable client source IP preservation:

```diff
- service.externalTrafficPolicy: Cluster
+ service.externalTrafficPolicy: Local
```

- PVC Access Mode:

```diff
- persistence.accessMode: ReadWriteOnce
+ ## To use the /admin portal and to ensure you can scale wordpress you need to provide a
+ ## ReadWriteMany PVC, if you dont have a provisioner for this type of storage
+ ## We recommend that you install the nfs provisioner and map it to a RWO volume
+ ## helm install nfs-server stable/nfs-server-provisioner --set persistence.enabled=true,persistence.size=10Gi
+ ##
+ persistence.accessMode: ReadWriteMany
```

- Start a side-car prometheus exporter:

```diff
- metrics.enabled: false
+ metrics.enabled: true
```

Note that [values-production.yaml](values-production.yaml) includes a replicaCount of 3, so there will be 3 WordPress pods. As a result, to use the "/admin" portal and to ensure you can scale wordpress you need to provide a ReadWriteMany PVC, if you don't have a provisioner for this type of storage, we recommend that you install the NFS provisioner chart (with the correct parameters, such as `persistence.enabled=true` and `persistence.size=10Gi`) and map it to a RWO volume.

Then you can deploy WordPress chart using the proper parameters:

```console
persistence.storageClass=nfs
mariadb.master.persistence.storageClass=nfs
```

### Sidecars

If you have a need for additional containers to run within the same pod as WordPress (e.g. an additional metrics or logging exporter), you can do so via the `sidecars` config parameter. Simply define your container according to the Kubernetes container spec.

```yaml
sidecars:
- name: your-image-name
  image: your-image
  imagePullPolicy: Always
  ports:
  - name: portname
   containerPort: 1234
```

If these sidecars export extra ports, you can add extra port definitions using the `service.extraPorts` value:

```yaml
service:
...
  extraPorts:
  - name: extraPort
    port: 11311
    targetPort: 11311
```

### Using an external database

Sometimes you may want to have Wordpress connect to an external database rather than installing one inside your cluster, e.g. to use a managed database service, or use run a single database server for all your applications. To do this, the chart allows you to specify credentials for an external database under the [`externalDatabase` parameter](#parameters). You should also disable the MariaDB installation with the `mariadb.enabled` option. For example with the following parameters:

```console
mariadb.enabled=false
externalDatabase.host=myexternalhost
externalDatabase.user=myuser
externalDatabase.password=mypassword
externalDatabase.database=mydatabase
externalDatabase.port=3306
```

Note also if you disable MariaDB per above you MUST supply values for the `externalDatabase` connection.

The above parameters map to the env variables defined in [bitnami/wordpress](http://github.com/bitnami/bitnami-docker-wordpress). For more information please refer to the [bitnami/wordpress](http://github.com/bitnami/bitnami-docker-wordpress) image documentation.

