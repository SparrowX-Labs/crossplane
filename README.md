# Crossplane compositions

Crossplane definitions for provisioning application-owned AWS resources from Kubernetes. The `XApplicationInfrastructure` composite resource creates immutable ECR repositories and, when enabled, PostgreSQL RDS databases, security groups, subnet groups, Secrets Manager credentials, and related records.

The `dev/` and `prod/` manifests describe the same service set in separate namespaces on the same EKS cluster. Stateful APIs enable their dedicated databases; the frontend and reporting service remain stateless. Argo CD owns synchronization, while the repository workflow detects changed environment manifests and requests the matching Argo CD sync.

## Workflow configuration

The repository inherits `AWS_ACCOUNT_ID`, `AWS_REGION`, and `AWS_ROLE_NAME` through the shared platform configuration and uses GitHub OIDC rather than static AWS keys. Its Argo CD sync workflow receives the organization secrets `ARGOCD_SERVER` and `ARGOCD_AUTH_TOKEN`. The Crossplane values files are the service-level inputs; AWS database credentials are generated and managed by the Crossplane composition through Secrets Manager.

## License

See [LICENSE.md](LICENSE.md).
