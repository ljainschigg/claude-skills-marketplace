# Configure MSR for OIDC authentication

After you register the application in Microsoft Entra ID, configure OIDC in MSR.

1. Navigate to **Administration** → **Configuration** → **Authentication**.
2. Set the **Auth Mode** to **OIDC**. 
3. Configure the following settings:

    - **OIDC Provider Name**: Specify the name that will display on the login page button.
    - **OIDC Endpoint**:
        1. In the Entra ID application, navigate to the **Overview** page.
        2. Open the application endpoints and locate the **OpenID Connect metadata document** value. Open this URL in a web browser.
        3. Copy the `issuer` value from the JSON document and use it as the endpoint URL.

    - **OIDC Client ID**: Enter the **Application (client) ID** from the Entra ID 
      application registration.
    - **OIDC Client Secret**: Enter the **Value** of the client secret from the 
      Entra ID application. 

        !!! note

            The client secret value is displayed only at creation time,
            thus if the value is hidden, delete the secret and create a new one.

    - **OIDC Scope**: Set this to `openid,profile,email,offline_access`.  
      Ensure these scopes are enabled in the API permissions for the application.

4. Save the configuration and click **Test OIDC Server** to verify connectivity.

## Test OIDC Login

After you complete the OIDC configuration in Entra ID and MSR, test the OIDC login.

1. Log out of the current MSR session. 
2. On the login page, select the button for the OIDC provider.
3. Log in with a user from the external tenant.
