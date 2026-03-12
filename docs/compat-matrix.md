# Release Compatibility Matrix

The following table lists the key software components and versions that have
been tested and validated by Mirantis for compatibility with MSR.

## Runtime Compatibility Matrix

| MSR    | Kubernetes required | Compatible MKE versions | Compatible MCR versions |
|--------|---------------------|-------------------------|-------------------------|
| 4.13.4 | 1.31–1.32           | 3.8.x, 4.1.x            | 25.x                    |
| 4.13.3 | 1.31–1.32           | 3.8.x, 4.1.x            | 25.x                    |
| 4.13.2 | 1.31–1.32           | 3.8.x, 4.1.x            | 25.x                    |
| 4.13.1 | 1.31–1.32           | 3.8.x, 4.1.x            | 25.x                    |
| 4.13.0 | 1.31–1.32           | 3.8.x, 4.1.x            | 25.x                    |

## Components Compatibility

| **Component** | **Chart / App Version** |
|----------------|--------------------------|
| **Postgres Operator** | Chart: 1.14.0<br>App: 1.14.0 |
| **PostgreSQL** | v17<br>Pod Image: `ghcr.io/zalando/spilo-17:4.0-p2` |
| **Redis Operator** | Chart: 0.20.3<br>App: 0.20.2 |
| **Redis** | Chart: `redis-replication`<br>App: 0.16.7 |
