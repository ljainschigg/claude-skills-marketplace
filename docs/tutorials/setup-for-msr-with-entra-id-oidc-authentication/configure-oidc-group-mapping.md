# Configure OIDC group mapping

To use the group membership function, configure both MSR and Entra ID.

## Entra ID configuration

Complete the following tasks in Entra ID.

### Assign groups to the OIDC application

Assign groups from the external tenant to the application. This configuration 
exposes groups by display name rather than the default group ID. Because MSR
cannot map IDs to aliases, it uses the Entra ID group name as the group name in MSR.

1. Open the [application you created](set-up-entra-id.md#create-an-external-tenant) when you set up the Entra ID.
2. Navigate to the **Users and Groups** page. This page is specific to the 
   application and is distinct from the tenant **Users** or **Groups** pages.
3. Click **Add user/group**.
4. Click the **None Selected** link under **Users and Groups**.
5. Add the tenant groups that are required for MSR team linkages. Note that you only need to add 
   groups, not individual users.

### Create a group claim in the OIDC configuration

Create a group claim and expose group display names in the token:

1. In the application registration, navigate to the **Token configuration** page.
2. Click **Add groups claim**.
3. Select **Groups assigned to the application** and save.
4. Navigate to the **Manifest** page.
5. Locate the `optionalClaims` section.
6. Within `optionalClaims`, locate the `idToken` array.
7. Ensure that `additionalProperties` includes the `cloud_displayname` value.

!!! warning

    Incorrect manifest edits can break authentication.

Section example:

```json
"idToken": [
  {
    "additionalProperties": [
      "cloud_displayname"
    ],
    "essential": false,
    "name": "groups",
    "source": null
  }
]
```

For more information, refer to the official Microsoft documentation: [Configure optional claims](https://learn.microsoft.com/en-us/entra/identity-platform/optional-claims).

## MSR configuration

After configuring group claims in Entra ID, configure MSR to read the
group information from the OIDC token.

### Add group claim name to authentication settings

Configure MSR to expect group information during login:

1. Navigate to **Administration** → **Configuration** → **Authentication**.
2. Set **Group Claim Name** to `groups`. This value must match the
   claim name in the ID token.
3. Save the configuration.

### Test group membership of a user

MSR assigns users to groups during login based on the group claims in
the OIDC token.

Users are already members of groups in Entra ID. When they log in, MSR
reads the group names from the token. If a group does not exist in MSR,
it is created automatically. If a group already exists and its name
matches the OIDC group name, MSR assigns the user to that group at
login.

Administrators can also create groups manually. If a manually created
group name matches an OIDC group name, MSR assigns users to that group
during login.

Verify the group linkage:

1. Ensure the **Groups** page is empty before testing to allow the login flow
   to create the groups. Do not create any groups manually in MSR. 
2. Log in to MSR as an OIDC user who belongs to a group in Entra ID.
3. The user page in MSR does not display group memberships, so log out.
4. Log back in to MSR as an administrator user.
5. Navigate to the **Groups** page. The group that corresponds to the Entra ID
   group should now appear.

You can now assign project permissions to the group.
OIDC users receive access based on the permissions assigned to that group.

!!! warning

    As new groups are created whenever a specified group does not exist
    in MSR, this can result in unintended groups. Thus, confirm that the
    group exists by using the auto-complete feature in the group name
    field.
