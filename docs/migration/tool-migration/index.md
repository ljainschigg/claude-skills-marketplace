# Tool Migration

This guide provides step-by-step instructions for migrating artifacts  
from **Mirantis Secure Registry (MSR)** versions **2.9** and **3.1** to  
**MSR 4** using the official migration tool.

The migration follows an **A/B model**, where your existing MSR deployment  
remains active while data is copied to a new MSR 4.x instance. The migration  
tool operates independently on a host with network access to both environments,  
ensuring operational continuity and minimizing risk.

**Key characteristics of the migration:**

- Migration is non-disruptive until the final cutover.  
- Metadata is transferred using offline copies for consistency.  
- The database backend changes from **RethinkDB** to **PostgreSQL**.  
- Team names and repository paths may change — pipelines may require updates.  
- Image data migration time depends on image count, size, and environment  
  performance; plan accordingly to manage load or perform immediate migration.  
- To minimize downtime during final cutover, repeat image migration to reduce  
  the remaining delta before the last sync.

!!! note
    Before starting migration, review:
    - [MSR 4 Key Changes](../../whats-new/index.md) for MSR 4 behavioral changes.  
    - [Removed features](../../whats-new/removed-features.md) and
      [What to Expect During the Migration](what-to-expect-when-transitioning.md)
      if you use Swarm, custom signing, or repository permissions.  
    - Contact Mirantis support if additional guidance is necessary.

## Tool Migration Contents

| Step                                                                                                       | Description |
|------------------------------------------------------------------------------------------------------------|--------------|
| [What to Expect During the Migration](what-to-expect-when-transitioning.md)                                | Summarizes major behavioral and architectural changes between MSR versions. Review before planning your migration timeline. |
| [Migration Prerequisites](migration-prerequisites.md)                                                      | Lists technical requirements for running the migration tool successfully. |
| [Install Migration Tool](install-migration-tool.md)                                                        | Explains how to download, verify, and install the migration tool on your migration host. |
| [Database Access Configuration](db-configuration.md)                                                       | Describes configuration for source and destination databases. |
| [Configure Migration Settings](configure-migration-settings.md)                                            | Guides configuration of the target environment for migration. |
| [Perform Migration](perform-tool-migration.md)                                                             | Details how to export from source MSR and import into the new MSR 4 deployment. |
| [Migrate Projects](partial-tool-migration/migrate-projects.md)                                             | Describes project migration steps. |
| [Migrate Permissions](partial-tool-migration/migrate-permissions.md)                                       | Describes how to migrate permissions and roles. |
| [Migrate Push and Poll Mirroring Policies](partial-tool-migration/migrate-push-poll-mirroring-policies.md) | Explains how to migrate mirroring policies. |
| [Validate Migration Data](validate-migration-data.md)                                                      | Provides optional verification steps to ensure successful migration of repositories, metadata, and configurations. |
| [Post-Migration Configuration](tool-configure-migration.md)                                                | Covers updates to pipelines, credentials, and access controls in MSR 4. |
| [Post-Migration Cleanup](clean-up-after-migration.md)                                                      | Lists cleanup steps, including decommissioning old MSR and freeing temporary resources. |
| [Migration Tool Reference](migration-tool-reference/index.md)                                                       | Contains CLI options and configuration parameters for the migration tool. |
| [Migration Tool Release Notes](migration-tool-release-notes/index.md)                                      | Provides release notes for the migration tool. |
