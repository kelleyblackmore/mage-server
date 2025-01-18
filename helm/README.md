### Deploying to a Kubernetes Cluster

This directory contains Helm charts for deploying MAGE services to a Kubernetes cluster.

## Prerequisites
- Kubernetes cluster (1.16+)
- Helm 3.0+
- kubectl configured to communicate with your cluster

## Installation Steps

1. Install the chart from the current directory:
```bash
helm install mage ./helm/auth-idp/auth-idp-chart
```

2. To customize the installation, create a values.yaml file and specify override values:
```yaml
image:
  repository: mage/server
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 4242

ingress:
  enabled: true
  className: nginx
  hosts:
    - host: mage.local
      paths:
        - path: /
          pathType: Prefix
```

Then install with:
```bash
helm install mage ./helm/auth-idp/auth-idp-chart -f values.yaml
```

3. Verify the deployment:
```bash
kubectl get pods
kubectl get services
```

## Container images

Container images are located under the docker folder and include:
- auth-idp: Authentication service
- server: Main MAGE server
- web: Web frontend

## Configuration

Key configuration options:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Image repository | `mage/server` |
| `image.tag` | Image tag | `latest` |
| `service.type` | Service type | `ClusterIP` |
| `service.port` | Service port | `4242` |

For additional configuration options, see the values.yaml file in the chart directory.