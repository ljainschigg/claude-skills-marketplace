# Release Compatibility Matrix

The following table lists the key software components and versions that have
been tested and validated by Mirantis for compatibility with MSR.

| **Component** | **Chart / App Version** |
|----------------|--------------------------|
| **Postgres Operator** | Chart: 1.14.0<br>App: 1.14.0 |
| **PostgreSQL** | v17<br>Pod Image: `ghcr.io/zalando/spilo-17:4.0-p2` |
| **Redis Operator** | Chart: 0.20.3<br>App: 0.20.2 |
| **Redis** | Chart: `redis-replication`<br>App: 0.16.7 |
| **Kubernetes** | v1.31<br>Included in MKE 3.8; also met by MKE 4. |

