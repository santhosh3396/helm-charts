# Helm Charts

Production-grade Helm charts for deploying microservices on Kubernetes with environment-specific value overrides.

## Charts

| Chart | Description |
|-------|-------------|
| `flask-app` | Flask Python application with HPA, Ingress, ConfigMap |

## Chart Structure

```
flask-app/
├── Chart.yaml              # Chart metadata
├── values.yaml             # Default values
├── values-dev.yaml         # Dev environment overrides
├── values-prod.yaml        # Production overrides
└── templates/
    ├── deployment.yaml     # Deployment with probes + resources
    ├── service.yaml        # ClusterIP service
    ├── configmap.yaml      # Environment config
    ├── hpa.yaml            # HPA (CPU + Memory)
    └── ingress.yaml        # NGINX Ingress
```

## Key Features

- Parameterized templates using Helm values
- Environment-specific overrides (dev / prod)
- HPA with CPU and Memory metrics (toggleable)
- Ingress with conditional TLS
- ConfigMap injection into Deployment
- Rolling update strategy with zero downtime

## Install Commands

```bash
# Install with default values
helm install flask-release ./flask-app

# Install for dev environment
helm install flask-dev ./flask-app -f flask-app/values-dev.yaml

# Install for production
helm install flask-prod ./flask-app -f flask-app/values-prod.yaml

# Upgrade existing release
helm upgrade flask-release ./flask-app --set image.tag=v2.0

# Dry run (validate before install)
helm install flask-release ./flask-app --dry-run --debug

# Uninstall
helm uninstall flask-release
```

## Verify

```bash
helm list
kubectl get all
kubectl get hpa
kubectl get ingress
```
