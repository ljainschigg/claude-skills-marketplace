# Set up Entra ID

After you install MSR, use an external tenant in Microsoft Entra ID to provide
a self-contained directory and add users and groups for testing. 

## Create an external tenant

For testing purposes, create a new external tenant.
For detailed information on how to do so, refer to the official [Microsoft External Tenant Quickstart](https://learn.microsoft.com/en-us/entra/external-id/customers/quickstart-tenant-setup).
After the setup is complete, create users and groups for testing. 
Ensure that you add users to the appropriate test groups.

## Register an application for OIDC authentication

To enable OIDC authentication for MSR, register an application.
Create a custom (non-gallery) enterprise application and configure it for OIDC.
For detailed information on how to do so, refer to the official Microsoft tutorial:
[Configure OIDC SSO for custom (non-gallery) applications](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-setup-oidc-sso#configure-oidc-sso-for-custom-non-gallery-applications).

Tutorial considerations:

- When you configure the application settings in the identity provider,
  set the **Redirect URI** to the value generated during [the Retrieve redirect URI](install-msr.md#retrieve-the-redirect-uri) process.

- After you create a client secret, copy the secret **Value**. Do not copy
  the **Secret ID**, as MSR requires the secret value itself for the OIDC
  **Client Secret** field in MSR.

- When you configure API permissions, enable all available
  OpenID-related permissions displayed in the web UI.

- After enabling all OpenID-related permissions, you can skip configuring the
  other fields listed in the tutorial for now. These additional values will be
  completed later during the final OIDC setup in MSR.

After you complete the application registration in the identity
provider portal, return to MSR to finish the OIDC setup.
