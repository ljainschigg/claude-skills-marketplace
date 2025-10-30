# Product highlights

This section summarizes the major architectural and functional improvements
introduced in MSR 4. These enhancements are designed to increase performance,
improve scalability, simplify operations, and align the platform with current
cloud-native standards.

## Quota Management

* Introduces project- and repository-level quotas.
* Administrators can enforce storage usage limits across teams.
* Helps prevent uncontrolled registry growth in shared environments.

## Expanded Replication Targets

* MSR 4 extends support for replicating images and artifacts to and from
  OCI-compatible registries.
* Supported targets include:

  * Docker Hub, Docker Registry v2
  * AWS Elastic Container Registry (ECR), Azure ACR
  * Google Container Registry (GCR), Google Artifact Registry
  * AliCloud Container Registry, Huawei SWR, GitLab, Quay, JFrog Artifactory

* Enables hybrid and multi-cloud workflows with minimal configuration.

## Modern Image Signing with Cosign and Notary v2

* Replaces Docker Content Trust (DCT) and Notary v1 with Cosign and Notary v2.
* Cosign and Notary v2 support OCI-native signature formats and validation.
* Signatures are stored alongside artifacts, improving integrity enforcement.
* Enables keyless signing using OIDC identities.
* Aligns with modern DevSecOps practices and cloud-native toolchains.

## Enhanced Backup and Restore with Velero

* Integrates Velero for backup and disaster recovery.
* Supports full and selective repository restoration.
* Compatible with AWS, GCP, Azure, and S3-compatible storage.
* Enables point-in-time recovery and incremental backups.

## SBOM Support (SPDX and CycloneDX)

* Supports storage and distribution of Software Bills of Materials (SBOMs).
* SPDX and CycloneDX formats are treated as first-class OCI artifacts.
* Enables automated compliance checks and dependency transparency.

## Modern Image Signing with Cosign

* Replaces Docker Content Trust (DCT) and Notary v1 with Cosign and Notary v2.
* Supports signing via OIDC without external signing services.
* Enables signature validation and artifact integrity with OCI standards.
* Enhances integration with Kubernetes-native DevSecOps workflows.

## Proxy Caching with Bandwidth Throttling

* Integrates Harbor's proxy cache for upstream image caching.
* Reduces bandwidth usage and improves image pull performance.
* Administrators can apply speed limits to control network usage.

## Enhanced Audit Logging and Observability

* Captures detailed audit logs for UI and API-level actions.
* Logs include user activity, system events, and admin operations.
* Uses structured formats compatible with centralized logging and SIEM tools.

## CloudNativeAI Model Registry Support

* Supports OCI-format storage for ML models via the CloudNativeAI format.
* Unifies container and model artifact management under a single registry.
* Enables version control and secure distribution of AI/ML models.

## Image Preheating with Dragonfly or Kraken

* Supports image preheating using Dragonfly or Kraken.
* Frequently used images are pulled to nodes in advance.
* Reduces deployment startup times for large workloads.
* Dragonfly provides peer-to-peer distribution across clusters.
