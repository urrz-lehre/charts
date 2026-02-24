# charts

A collection of [Helm](https://helm.sh) charts created by us. This repository provides well-documented and configurable Helm charts following cloud-native best practices.

## Quick Start

### Prerequisites

- Kubernetes 1.24+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is enabled)

### Installing Charts

In order to use the charts provided, simply add this repository to helm and install:

```sh
helm repo add urrz-lehre https://urrz-lehre.github.io/charts/
helm install <name> urrz-lehre/<chart>
```

## Configuration

Each chart provides extensive configuration options through `values.yaml`. Key configuration areas include:

- **Authentication & Security**: User credentials, existing secrets, security contexts
- **Storage**: Persistent volumes, storage classes, backup configurations
- **Networking**: Services, ingress, network policies
- **Scaling**: Replica counts, autoscaling, resource limits

Refer to individual chart READMEs for detailed configuration options.

## Contributing

This repository is a read-only mirror of an existing repository on our existing private GitLab instance. Regardless, please send your pull requests through GitHub. We will then approve of them here, but will push them separately on GitLab, which will then be mirrored back through GitHub.

One important note: All of our `README.md` files located within the separate charts were generated using [helm-docs](https://github.com/norwoodj/helm-docs).
Please make sure to regenerate the documentation once your changes are implemented!

### Chart Issues

For issues specific to these Helm charts:

- Check individual chart README files for troubleshooting
- Review chart documentation and examples
- Verify configuration values
- Open an issue on GitLab
