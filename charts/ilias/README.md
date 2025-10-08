# ilias Helm chart

![Version: 0.1.1](https://img.shields.io/badge/Version-0.1.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

ilias-helm is a [Helm](https://helm.sh) chart for installing [ilias](https://ilias.org).

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://ghcr.io/dragonflydb/dragonfly/helm | dragonfly | v1.25.1 |
| oci://registry-1.docker.io/cloudpirates | postgres | 0.7.2 |

## Installation and configuration

As this chart repository is not public, you'll need to generate an Access Token in order to access it. Refer to the README located at the root of this repository for instructions.

1. (Optional) if you want to deploy this chart in a separate `Namespace`, make sure to create that:

    ```sh
    kubectl create namespace <YOUR-NAMESPACE>
    ```

2. Using `examples/image-pull-secret.yaml`, create a new `Secret` containing the pull secret for your ilias container image. Adjust this file to your liking, then apply using:

    ```sh
    kubectl apply -f examples/image-pull-secret.yaml
    ```

3. (Optional) using `examples/postgres-auth.yaml`, create a new `Secret` containing the access credentials for Postgres. Adjust this file to your liking, then apply using:

    ```sh
    kubectl apply -f examples/postgres-auth.yaml
    ```

4. Copy and adjust the `values.yaml` file of this chart to fit your needs.

5. Install this Helm chart by running:

    ```sh
    helm install -n <YOUR-NAMESPACE> -f <YOUR-VALUES> referat-lehre/ilias
    ```

6. ilias should now be deployed on your Kubernetes cluster. You can verify this using tools like [K9s](https://k9scli.io). We recommend finalizing the installation by opening a shell on the ilias pod and running:

    ```sh
    php admin/cli/install.php
    ```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Specifies on which types of nodes this pod shall run. |
| autoscaling.enabled | bool | `false` | Enables/Disables Autoscaling. |
| autoscaling.maxReplicas | int | `100` | Maximum amount of replicas to spawn. |
| autoscaling.minReplicas | int | `1` | Minimum amount of replicas to spawn. |
| autoscaling.targetCPUUtilizationPercentage | int | `80` | Target CPU usage (in percent) the pod has to reach before spawning another one. |
| cron.commands | list | `[["/usr/local/bin/php","/var/www/html/admin/cli/cron.php","--keep-alive=59"],["/usr/local/bin/php","/var/www/html/admin/cli/adhoc_task.php","--execute","--keep-alive=59"]]` | Commands to run for CronJob. |
| cron.enabled | bool | `true` | Enables / Disables the CronJob. |
| cron.schedule | string | `"*/5 * * * *"` | Schedule for the CronJob. |
| dragonfly.enabled | bool | `true` | Enables / Disables Dragonfly. |
| dragonfly.extraArgs | list | `["--dbfilename=dump","--snapshot_cron=* * * * *"]` | Extra Parameters for Dragonfly. |
| dragonfly.podSecurityContext | object | `{}` | SecurityContext for Dragonfly pod. |
| dragonfly.securityContext | object | `{}` | SecurityContext for Dragonfly containers. |
| dragonfly.storage.enabled | bool | `true` | Enables / Disables persistence for Dragonfly. |
| dragonfly.storage.requests | string | `"128Mi"` | PersistentVolumeClaim size for Dragonfly. |
| fullnameOverride | string | `""` | String to fully override ilias.fullname. |
| image.pullPolicy | string | `"IfNotPresent"` | ilias image pull policy. |
| image.repository | string | `"ghcr.io/iliashq/ilias-php-apache"` | ilias image repository. |
| image.tag | string | `"8.4-bookworm"` | ilias image tag. |
| imagePullSecrets | list | `[]` | Names of secret required for pulling image. |
| ingress.annotations | object | `{}` | Additional annotations for ilias ingress. |
| ingress.className | string | `""` | ClassName for ilias ingress. |
| ingress.enabled | bool | `false` | Enables / Disables ilias ingress. |
| ingress.hosts[0] | object | `{"host":"chart-example.local","paths":[{"path":"/","pathType":"ImplementationSpecific"}]}` | Hostname for ilias ingress. |
| ingress.hosts[0].paths[0] | object | `{"path":"/","pathType":"ImplementationSpecific"}` | Path for ilias ingress. |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` | PathType for ilias ingress. |
| ingress.tls | list | `[]` | TLS configuration for ilias ingress. |
| init.enabled | bool | `true` | Enables / Disables the init container. |
| livenessProbe.httpGet.path | string | `"/"` | Path to use for ilias pod LivenessProbe. |
| livenessProbe.httpGet.port | string | `"http"` | Port to use for ilias pod LivenessProbe. |
| nameOverride | string | `""` | String to partially override ilias.fullname. |
| nodeSelector | object | `{}` | Specifies on which node this pod shall run. |
| persistence.accessModes | list | `["ReadWriteOnce"]` | AccessModes for ilias PersistentVolumeClaim. |
| persistence.enabled | bool | `true` | Enables / Disables persistence for ilias. |
| persistence.size | string | `"8Gi"` | Size of ilias PersistentVolumeClaim. |
| podAnnotations | object | `{}` | Additional annotations for ilias pod |
| podLabels | object | `{}` | Additional labels for ilias pod. |
| podSecurityContext | object | `{}` | SecurityContext for ilias pod. |
| postgres.auth.database | string | `"ilias"` | Name of the database that Postgres shall create. |
| postgres.auth.username | string | `"ilias"` | Username of the database root user. |
| postgres.enabled | bool | `true` | Enables/Disables Postgres pod. |
| postgres.image.tag | string | `"17-alpine"` | Postgres tag the database container shall use. |
| postgres.persistence.accessModes | list | `["ReadWriteOnce"]` | AccessModes for Postgres PersistentVolumeClaim. |
| postgres.persistence.enabled | bool | `true` | Enables/Disables persistence for Postgres. |
| postgres.persistence.storageClassName | string | `"standard"` | StorageClass for Postgres PersistentVolumeClaim. |
| readinessProbe.httpGet.path | string | `"/"` | Port to use for ilias pod ReadinessProbe. |
| readinessProbe.httpGet.port | string | `"http"` | Port to use for ilias pod LivenessProbe. |
| replicaCount | int | `1` |  |
| resources | object | `{}` | Resource allocations for ilias pod. |
| securityContext | object | `{}` | SecurityContext for ilias containers. |
| service.ports | list | `[{"containerPort":80,"name":"http"},{"containerPort":443,"name":"https"}]` | Ports for ilias service, see [here](https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports). |
| service.ports[0] | object | `{"containerPort":80,"name":"http"}` | Name of first ilias service port. |
| service.ports[0].containerPort | int | `80` | Port within container that shall be used. |
| service.ports[1].containerPort | int | `443` | Port within container that shall be used. |
| service.type | string | `"ClusterIP"` | Service type for ilias service, see [here](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types). |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount's API credentials? |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. |
| tolerations | list | `[]` | Specifies what kinds of taints are tolerable for this pod. |
| volumeMounts | list | `[]` | Additional volumeMounts on the output Deployment definition. |
| volumes | list | `[]` | Additional volumes on the output Deployment definition. |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
