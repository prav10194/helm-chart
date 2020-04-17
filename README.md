# IBM_DC_ManageTo_IriusRisk
Helm Chart repository to setup IriusRisk security scan tool

Helm chart related artefacts are stored within "templates" directory and subdirectories.

Jenkins pipeline function is defined in "pushArtifactoryIriusRiskImages.groovy".

# Dependency Track Helm Chart

This directory contains a Kubernetes chart to deploy IriusRisk; consisting of Nginx, Tomcat & PostgreSQL.

## Prerequisites Details

* Kubernetes 1.6+

## Chart Details

This chart will do the following:

* Implement an IriusRisk deployment

## Installing the Chart

To install the chart, use the following:

```console
$ cd <PROJECT_FOLDER>
```

To download dependent charts
```console
$ helm dep build
```

```console
$ helm install <desired_release_name> ./
```

## Configuration

The following table lists the configurable parameters of the IriusRisk chart and their default values.

|             Parameter             |              Description                 |               Default               |
|-----------------------------------|------------------------------------------|-------------------------------------|
| `replicaCount`          | Number of replicas                               | `1`                      |
| `image.repository`           | Image respository name                       | `docker.io/owasp/dependency-track`                                 |
| `image.tag`           | Image respository tag                        | `3.7.1`                      |
| `image.pullPolicy`          | Pull policy                               | `IfNotPresent`      |
| `imagePullSecrets`          | Image pull secrets                      | `[]`      |
| `nameOverride`          | Override name                              | ``      |
| `fullnameOverride`               | Override full name                              | ``                              |
| `initContainers` | Init containers               | `[]`                                |
| `readinessProbe.initialDelaySeconds` | Initial delay seconds for readiness probe                     | `60`                      |
| `livenessProbe.initialDelaySeconds`               | Initial delay seconds for liveness probe              | `60`                                |
| `serviceAccount.create`         | Boolean create service account - used by _helpers.tpl      | `true`                             |
| `serviceAccount.name`       | Default Service account name to be used in case create is false                       | `"dependency-track"`                                |
| `testserviceAccount.name`       | Default Test Service account name to be used in case create is false                       | `"test-service-account"`   
| `podSecurityContext.fsGroup`        | Pod security context fsGroup                  | `1000`                      |
| `securityContext.capabilities.drop` | Security context capabilities drop               | `ALL`                                |
| `securityContext.readOnlyRootFilesystem` | Boolean read only root file system                    | `true`                      |
| `securityContext.runAsNonRoot`               | Boolean run as non root                | `""`                                |
| `securityContext.runAsUser`         | Run as user       | `1000`                             |
| `securityContext.runAsGroup`       | Run as group                        | `1000`                                |
| `service.type`        | Service type to be used              | `LoadBalancer` 
| `service.port`        | Service port                  | `8080` 
| `service.targetPort`        | Service target port                 | `8080` 
| `service.nodePort`        | Service node port - commented out              | `30008` 
| `ingress.enabled`        | Boolean ingress enabled - used by _helpers.tpl               | `true` 
| `ingress.annotations`        | Ingress annotations                  | `{}` 
| `ingress.hosts`        | Ingress hosts               | `dependencytrack.libertyopenshift.us-south.containers.appdomain.cloud` 
| `ingress.tls`        | tls                  | `[]` 
| `resources.requests.cpu`        | Requests cpu                  | `1500m` 
| `resources.requests.memory`        | Requests memory                 | `4Gi` 
| `resources.limits.cpu`        | Limits cpu                  | `4` 
| `resources.limits.memory`        | Limits memory                  | `16Gi` 
| `nodeSelector`        | Node selector                 | `{}` 
| `tolerations`        | Tolerations                 | `[]` 
| `affinity`        | Affinity                  | `{}` 
| `env`        | Env                  | `[]` 
| `persistentVolume.enabled`        | Boolean persistent volume enabled                  | `true` 
| `persistentVolume.size`        | Persistent volume size                  | `8Gi` 
| `persistentVolume.annotations`        | Persistent volume annotations                 | `{}` 
| `persistentVolume.storageClass`        | Persistent volume storage class                  | `""` 
| `emptyDir.sizeLimit`        | emptyDir size limit                 | `8Gi` 
| `configmap.application.properties`        | Application properties of configmap                  | `` 
| `postgresql.enabled`        | Boolean value of postgres enabled                | `true` 
| `postgresql.postgresqlUsername`        | Postgresql Username                  | `deptrack` 
| `postgresql.postgresqlPassword`        | Postgresql Password                  | `deptrack` 
| `postgresql.postgresqlDatabase`        | Postgresql Database                  | `deptrack` 

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.


## Remove Deployment

```console
$ helm delete IriusRisk --purge
```
or
```console
$ helm uninstall IriusRisk
```

## Accesing IriusRisk Console

```console
$ <some text>
```

Open a browser to _https://<CONSOLE_ADDRESS>:8080_, enter in a username and password as admin/admin. 

## Using minikube

Dependency track needs the following config to run on minikube 
```console
$ minikube start --vm-driver=hyperkit --cpus=4 --memory=8192
```

To access the service 
```console
$ minikube service -n dependency-track dependencytrack-dependency-track --url
```