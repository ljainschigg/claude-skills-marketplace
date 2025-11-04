# Changelog

MSR 4.13.0 comprises the Harbor 2.13 upstream release. It also includes changes from the intermediate upstream 2.11 and 2.12 releases, for which there was no separate MSR release.

## Changes specific to MSR

- **[MSRH-162]** LDAP Group Admin now supports nested groups in a search filter.  
- **[MSRH-189]** Docker Compose installation packages have been updated to reference `msr` instead of `harbor`.  
- **[MSRH-194]** The Helm chart has been updated to reference `msr` and `Mirantis` instead of `harbor`.  
- **[MSRH-242]** Mirantis now recommends the following operators for deploying PostgreSQL and Redis in high availability (HA) mode:
  - PostgreSQL: `zalando/postgres-operator`
  - Redis: `OT-CONTAINER-KIT/redis-operator`

## Changes from upstream

The following upstream pull requests and features are relevant to MSR.  
For complete upstream details, refer to:

- [Harbor 2.11.0 Release Notes](https://github.com/goharbor/harbor/releases/tag/v2.11.0)
- [Harbor 2.12.0 Release Notes](https://github.com/goharbor/harbor/releases/tag/v2.12.0)
- [Harbor 2.13.0 Release Notes](https://github.com/goharbor/harbor/releases/tag/v2.13.0)

### What’s New

- **SBOM Generation and Management:**  
  Harbor now supports generating Software Bill of Materials (SBOM) both
  manually and automatically. Users can view, download, and replicate SBOMs
  across multiple Harbor instances.

- **OCI Distribution Spec v1.1.0 Support:**  
  Harbor now fully supports [OCI Distribution Spec v1.1.0](https://github.com/opencontainers/distribution-spec/tree/v1.1.0).

- **VolcEngine Registry Integration:**  
  Added support for replicating images to and from the VolcEngine registry.

- **Enhanced Robot Account Management:**  
  Improved robot account functionality enhances access control and automates
  CI/CD processes.

- **Proxy Cache Speed Limit:**  
  Allows administrators to set bandwidth limits for proxy cache projects.

- **Improved LDAP Onboarding:**  
  Faster LDAP user onboarding and better authentication performance.

- **ACR & ACR EE Registry Integration:**  
  Added replication support for Azure Container Registry (ACR) and ACR
  Enterprise Edition.

- **Extended Audit Logging:**  
  Provides more detailed user action and API logging with improved query
  performance.

- **Enhanced OIDC Integration:**  
  Adds user session logout and PKCE (Proof Key for Code Exchange) support.

- **CloudNativeAI Integration:**  
  Enables management, versioning, and retrieval of AI models directly in Harbor.

- **Redis TLS Support:**  
  Adds secure Redis communication with TLS encryption for data in transit.

- **Enhanced Dragonfly Preheating:**  
  Supports additional parameters, customizable scopes, and cluster ID targeting
  for optimized image distribution.

### Deprecations

- **Removed:** robotV1 from the code base  
  ([#20991](https://github.com/goharbor/harbor/pull/20991)) by @sgaist

### Breaking Changes

- **Update CSRF key generation**  
  ([#21154](https://github.com/goharbor/harbor/pull/21154)) by @wy65701436  
- **Remove with_signature**  
  ([#21420](https://github.com/goharbor/harbor/pull/21420)) by @wy65701436

### Enhancements

- Enable `MAX_JOB_DURATION_SECONDS` in the jobservice container  
  ([#21232](https://github.com/goharbor/harbor/pull/21232)) by @stonezdj  
- Extend P2P preheat policy  
  ([#21115](https://github.com/goharbor/harbor/pull/21115)) by @chlins  
- Fix replication rule message in UI  
  ([#21299](https://github.com/goharbor/harbor/pull/21299)) by @bupd  
- Add `execution_id` and `task_id` to replication webhook payload  
  ([#21614](https://github.com/goharbor/harbor/pull/21614)) by @chlins  
- Add audit log support  
  ([#21377](https://github.com/goharbor/harbor/pull/21377)) by @xuelichao  
- Revamp Copy Pull Command  
  ([#21155](https://github.com/goharbor/harbor/pull/21155)) by @bupd  
- Add PKCE support for OIDC authentication  
  ([#21702](https://github.com/goharbor/harbor/pull/21702)) by @reasonerjt  
- Add Persistent Page Size UI  
  ([#21627](https://github.com/goharbor/harbor/pull/21627)) by @bupd  
- Add list project artifacts API  
  ([#20803](https://github.com/goharbor/harbor/pull/20803)) by @wy65701436  
- Export Harbor statistics as Prometheus metrics  
  ([#18679](https://github.com/goharbor/harbor/pull/18679)) by @tpoxa  
- Refactor P2P preheat Dragonfly driver  
  ([#20922](https://github.com/goharbor/harbor/pull/20922)) by @chlins  
- Enable build of the spectral image on ARM  
  ([#20506](https://github.com/goharbor/harbor/pull/20506)) by @Vad1mo  
