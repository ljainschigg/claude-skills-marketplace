# Inspect OIDC responses

To debug OIDC integration issues, review the responses that Microsoft Entra ID sends to MSR.
Use the [OpenID Connect](https://www.openidconnect.net) test tool to simulate the OIDC flow.

Before you begin, complete the [OIDC application registration](set-up-entra-id.md#register-an-application-for-oidc-authentication) in Entra ID.

## Set up the tutorial

!!! warning

    The OpenID Connect test tool does not persist the **Client ID**
    and **Client Secret** when advancing to **Set the OIDC Client ID** of the flow.
    Manually re-enter the values in the **Request** box to continue. Each time 
    you restart the authentication flow from the beginning, re-enter the 
    **Client ID** and **Client Secret** in the Configuration section.

On the OpenID Connect page, open the **Configuration** section and set the
following values.

**Set the Discovery Document URL:**

1. In the Microsoft Entra ID application registration, open
   **Endpoints**.
2. Copy the **OpenID Connect metadata document** URL.
3. Paste the URL into the **Discovery Document URL** field on the tutorial page.
4. Click **Use**.

**Set the OIDC Client ID:**

1. In the application registration, copy the **Application (client) ID**.
2. Paste the value into the OIDC **Client ID** field on the tutorial page.

**Set the OIDC Client Secret:**

1. In the application registration, open **Certificates & secrets**.
2. Create a new **Client Secret** for testing. Do not reuse a
   production secret, as this could compromise security.
3. Copy the **Value**. Do not use the **Secret ID**.
4. Paste the value into the OIDC **Client Secret** field on the tutorial page.

**Add the OpenID Connect callback URL:**

1. From the OpenID Connect **Configuration** section, copy the
   displayed callback URL, for example
   `https://openidconnect.net/callback`.
2. In the Entra ID application registration, open **Authentication**.
3. Under the **Web Redirect URIs**, add an entry for the callback URL
   and save.
