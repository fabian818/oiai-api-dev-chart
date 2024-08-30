# Helm Chart for oiai-backend

This Helm chart is used to deploy the `oiai-backend` service and manage its configurations. It integrates with ArgoCD for GitOps and uses the Helm chart built for `oiai-backend` to satisfy the CI/CD requirements. 

## Project Structure

``` bash
.
├── Chart.yaml         # Helm chart metadata
├── .argocd-source-api-dev.yaml # File uplodaded by argocd-image-updater
├── templates          # Templates for Kubernetes resources
│   ├── api-configmap.yml     # ConfigMap for API configuration
│   ├── api.yaml              # Deployment and Service for the API
│   └── haproxy-postgres.yaml # HAProxy configuration for PostgreSQL
└── values.yaml        # Default values for the Helm chart
```

## Features

- **Integration with ArgoCD**: Directly connected to ArgoCD for GitOps-based deployments.
- **Configurable**: Supports a wide range of configuration options through `values.yaml`.

## Usage

To deploy this Helm chart, follow these steps:

1. Install the argocd application referencing this repository.


2. Push commits to main branch in oiai-backend, then let arocd-image-updater to detect image change, and set the new version as the latest.


## Configuration

The configuration for this Helm chart is managed through the `values.yaml` file. Here is a sample configuration:

``` bash
api:
  image:
    repository: my-repo/oiai-backend
    version: 1.0.0
  databaseSecret: my-database-secret
  alb:
    certificateArn: 
```

### Values

- **api.image.repository**: The Docker image repository for the `oiai-backend` service.
- **api.image.version**: The version of the Docker image to use.
- **api.databaseSecret**: The secret containing database credentials.
- **api.alb.certificateArn**: The ARN of the SSL certificate for the Application Load Balancer (ALB).

## GitOps with ArgoCD

This Helm chart is designed to work with ArgoCD's image updater. ArgoCD monitors the Git repository for changes in Helm charts and automatically updates the deployed applications. 

### ArgoCD Integration

- The Helm chart is connected to ArgoCD through GitOps.
- The ArgoCD image updater ensures that the deployments are updated with the latest images from the repository.

## Notes

- The base chart uses a library chart, so it has numerous attributes and configuration options that can be adjusted as needed.
- Make sure to refer to the library chart's documentation for a comprehensive list of configurable attributes.

## Future Enhancements

- **Extended Documentation**: Provide more detailed configuration options and examples.
