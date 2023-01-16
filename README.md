# Helm Chart for ServiceA and ServiceB
This repository contain two helm charts, front-end-called serviceA, and back-end called serviceB
This Helm chart deploys a front-end service called ServiceA, which publishes hits to a NATS server and get number publishes from PostgreSql
This Helm chart deploys a back-end service called ServiceB, which listen hits on the NATS server and save those publishes on PostgreSql
each of the charts hase dependencies charts:

## Chart Details

- `apiVersion`: v2
- `description`: A Helm chart for Kubernetes
- `dependencies`:
  - name: postgresql
    repository: https://charts.bitnami.com/bitnami
    version: 12.1.9
  - name: nats
    repository: https://nats-io.github.io/k8s/helm/charts/
    version: 0.20.0
- `version`: 1.0.0

## Configuration

The following table lists the configurable parameters of the ServiceA chart and their default values.


| Value | Description | Default |
|-------|-------------|---------|
| replicaCount | Number of replicas for the deployment | 1 |
| image | Container image information | `repository: gcr.io/the-delight-365908/service_a`, `pullPolicy: IfNotPresent`, `tag: "v1.0"` |
| imagePullSecrets | Image pull secrets | `[]` |
| nameOverride | Override for the name of resources | "" |
| fullnameOverride | Override for the full name of resources | "" |
| serviceAccount | Configuration for the service account | `create: true`, `annotations: {}`, `name: ""` |
| podAnnotations | Pod annotations | `{}` |
| podSecurityContext | Pod security context | `{}` |
| securityContext | Security context | `{}` |
| service | Service configuration | `type: ClusterIP`, `port: 80` |
| ingress | Ingress configuration | `enabled: true`, `className: "nginx"`, `annotations: {kubernetes.io/ingress.class: nginx}`, `hosts: [{host: chart-example.local, paths: [{path: /, pathType: ImplementationSpecific}]}]`, `tls: []` |
| resources | Resource limits and requests | `{}` |
| autoscaling | Autoscaling configuration | `enabled: false`, `minReplicas: 1`, `maxReplicas: 100`, `targetCPUUtilizationPercentage: 80` |
| nodeSelector | Node selector | `{}` |
| tolerations | Tolerations | `[]` |
| affinity | Affinity | `{}` |
| postgresql | PostgreSQL configuration | `global: {postgresql: {auth: {username: "", password: "", database: ""}, service: {port: 5432}}}` |
| nats | NATS configuration | `global: {nats: {auth: {username: "", password: ""}, service: {port: 4222}}}` |

## Usage

To install the chart with the release name `my-release`:

'''

    $ helm install my-release serviceA/ -f value.yaml
    $ helm install my-release serviceB/ -f value.yaml
  
'''
