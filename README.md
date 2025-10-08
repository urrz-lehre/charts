# charts

A collection of [Helm](https://helm.sh) charts created by us. This repository provides well-documented and configurable Helm charts following cloud-native best practices.

## Quick Start

### Prerequisites

- Kubernetes 1.24+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is enabled)

### Installing Charts

In order to use the charts provided, you'll need to generate an [Access Token](./-/settings/access_tokens).

```sh
helm repo add referat-lehre \
--username gitlab-ci-token \
--password <ACCESS-TOKEN> \
https://gitlab.uni-regensburg.de/api/v4/projects/786/packages/helm/main/

helm install referat-lehre/<chart>
```

## Configuration

Each chart provides extensive configuration options through `values.yaml`. Key configuration areas include:

- **Authentication & Security**: User credentials, existing secrets, security contexts
- **Storage**: Persistent volumes, storage classes, backup configurations
- **Networking**: Services, ingress, network policies
- **Scaling**: Replica counts, autoscaling, resource limits

Refer to individual chart READMEs for detailed configuration options.

## Contributing

Want to contribute? Awesome! The most basic way to show your support is to star the project, or to raise issues.

One important note: All of our `README.md` files located within the separate charts were generated using [helm-docs](https://github.com/norwoodj/helm-docs).
Please make sure to regenerate the documentation once your changes are implemented!

### Chart Issues

For issues specific to these Helm charts:
- Check individual chart README files for troubleshooting
- Review chart documentation and examples
- Verify configuration values
- Open an issue on GitLab