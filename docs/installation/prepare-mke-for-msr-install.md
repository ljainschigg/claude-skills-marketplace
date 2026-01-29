# Prepare MKE for MSR Installation

MKE enforces security controls that can block MSR PostgreSQL deployments when
using the Zalando Postgres Operator. To meet MSR PostgreSQL security
requirements, configure MKE using a least-privilege approach.

## Preferred approach

Install the Zalando Postgres Operator with the Spilo privileges disabled.
MSR does not require privileged Postgres containers, so running Spilo in
unprivileged mode aligns with Kubernetes security best practices and
circumvents the need to modify the MKE admission policies.

1. Set the following values in the Postgres Operator Helm `values.yml` file:

    ```yaml
    configKubernetes:
      spilo_privileged: false
      spilo_allow_privilege_escalation: false
    ```
    
    | Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;     | Description                                                                                                                                                                                                 |
       |--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | `spilo_privileged`                         | Controls whether the Spilo container runs in Kubernetes `privileged` mode. Privileged containers have host-level access and bypass most container isolation. MSR Postgres does not require privileged mode. |
    | `spilo_allow_privilege_escalation`         | Controls whether the Spilo container can gain additional privileges (for example, through `setuid` binaries). MSR does not rely on OS-level privilege escalation.                                           |

    Mirantis recommends that you configure these parameters in the Helm values
    file rather than patching the MKE 4k validating admission policies,
    as MKE may revert the policies to their default values over time.

2. Install the Postgres Operator:

    ```
    helm install postgres-operator postgres-operator \
      --repo https://opensource.zalando.com/postgres-operator/charts/postgres-operator \
      -f postgres-operator-values.yaml
    ```

3. Verify the Postgres Operator configuration:

    ```bash
    kubectl get operatorconfiguration postgres-operator \
      -o custom-columns=NAME:.metadata.name,SPILO_APE:.configuration.kubernetes.spilo_allow_privilege_escalation,SPILO_PRIV:.configuration.kubernetes.spilo_privileged
    ```

    Example output:

    ```pgsql
    NAME                SPILO_APE   SPILO_PRIV
    postgres-operator   false       false
    ```

4. Confirm that the security settings were inherited:

    ```bash
    kubectl get sts msr-postgres \
      -o custom-columns=NAME:.metadata.name,SPILO_APE:'.spec.template.spec.containers[0].securityContext.allowPrivilegeEscalation',SPILO_PRIV:'.spec.template.spec.containers[0].securityContext.privileged'
    ```

    Example output:

    ```nginx
    NAME           SPILO_APE   SPILO_PRIV
    msr-postgres   false       false
    ```

## Alternative approaches

Mirantis recommends that you only use the MKE preparation approaches detailed
herein if your environment requires you to run Postgres containers with
elevated privileges.

Running Postgres with elevated privileges increases the security risk
surface. It is not required for standard MSR installations, and thus you 
should only consider it when a documented, environment-specific 
requirement prevents the use of the recommended least-privilege configuration.

### MKE 4k preparation

To install MSR on MKE 4k, you must modify the default validating admission
policy to allow for the required PostgreSQL resources.

Apply the following patch to update the `mke4-ucpauthz` validating admission
policy:

```bash
kubectl patch validatingadmissionpolicy mke4-ucpauthz --type=merge -p '
{
  "spec": {
    "matchConditions": [
      {
        "name": "skip-spilo-statefulsets",
        "expression": "!(request.userInfo.username == \"system:serviceaccount:default:postgres-operator\" && request.resource.group == \"apps\" && request.resource.resource == \"statefulsets\" && (request.operation == \"CREATE\" || request.operation == \"UPDATE\"))"
      },
      {
        "name": "skip-spilo-pods",
        "expression": "!(request.userInfo.username == \"system:serviceaccount:kube-system:statefulset-controller\" && request.operation == \"CREATE\" && request.resource.group == \"\" && request.resource.resource == \"pods\" && object.metadata.ownerReferences.exists(r, r.kind == \"StatefulSet\" && r.name == \"msr-postgres\"))"
      }
    ]
  }
}'
```

### MKE 3 preparation

To install MSR on MKE 3, you must first configure both the `default:postgres-operator`
user account and the `default:postgres-pod` service account in MKE 3 with the **privileged**
permission.

**To prepare MKE 3.x for MSR install:**

1. Log in to the MKE web UI.  

2. In the left-side navigation panel, click the **<username>** drop-down to display the available options.  

3. Click **Admin Settings > Privileges**.  

4. Navigate to the **User account privileges** section.  

5. Enter `<namespace-name>:postgres-operator` into the **User accounts** field.  

    !!! note

        You can replace `<namespace-name>` with `default` to indicate the use of the default namespace.  

6. Select the **privileged** checkbox.  

7. Scroll down to the **Service account privileges** section.  

8. Enter `<namespace-name>:postgres-pod` into the **Service accounts** field.  

    !!! note

        You can replace `<namespace-name>` with `default` to indicate the use of the default namespace.  

9. Select the **privileged** checkbox.  

10. Click **Save**.  

    !!! info
   
        For already deployed MSR instances, issue a rolling restart of the `postgres-operator` deployment:  
   
        ```bash
        kubectl rollout restart deploy/postgres-operator
        ```
