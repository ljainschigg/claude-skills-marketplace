# Removed features

The following capabilities available in previous MSR versions are not included
in MSR 4:

* **SAML Support**: MSR 4 no longer supports SAML authentication and instead
  uses OpenID Connect (OIDC), a more modern and flexible standard that better
  aligns with cloud-native environments and improves security and scalability.
  Refer to [OIDC Authentication](../operations/authentication-configuration/oidc-authentication.md)
  for more information on configuring OIDC.
* **Promotion Policies**: Automated promotion policies are no longer included.
  Customers can adapt their CI/CD pipelines to achieve similar workflows.
* **Swarm support** customers can use MSR 4 as a single instance for Swarm
  environments instead of HA clusters

# MSR Editions Feature Matrix

| **Feature** | **MSR 4 (Harbor-Based)** | **MSR2** | **MSR3** |
|--------------|--------------------------|-----------|-----------|
| **Distribution** | CNCF Harbor | Proprietary | Proprietary |
| **Database** | PostgreSQL | RethinkDB | RethinkDB |
| **Redis (Caching)** | Yes | Yes | Yes |
| **Orchestration** | Kubernetes-native | Docker Swarm | Docker Swarm |
| **OCI Compliance** | Full OCI and Helm OCI support | Limited support | Limited support |
| **User Interface** | Modern and intuitive | Basic | Improved |
| **Quotas** | Fully supported | Not available | Not available |
| **Vulnerability Scanning** | Trivy, Grype, Aqua, Anchore, and others | Synopsis (built-in) | Synopsis (built-in) |
| **Backup Integration** | Velero-based backup/restore | Manual/internal | Manual/internal |
| **Promotion Policies** | Not Available | Available | Available |
| **SAML Support** | Replaced by [OIDC](../operations/authentication-configuration/oidc-authentication.md) | Available | Available |
| **In-Place Upgrades** | Yes | No | No |
| **Image Signing** | Uses [Cosign](../operations/signing-artifacts-with-cosign.md) for image signing and verification | Uses Docker Content Trust (DCT) based on Notary v1 | Uses Docker Content Trust (DCT) based on Notary v1 |
| **Long Repository Names** | 256 characters | Limited | Limited |
| **SBOM Support** | SPDX, CycloneDX | Not available | Not available |
| **Artifact Replication** | Docker Hub, AWS ECR, GCR, GitLab, Quay, etc. | Limited | Limited |
| **Proxy Cache and Throttling** | Full support with bandwidth control | Not available | Not available |
| **Audit Logging** | Extended API/UI activity tracking | Basic | Basic |
| **AI Model Registry** | Supported via CloudNativeAI | Not available | Not available |
| **Preheat** | Dragonfly-based P2P preheat | Not available | Not available |


