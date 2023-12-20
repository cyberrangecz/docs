# Setting up OIDC Provider

KYPO CRP is from the release 23.12 deployed with Keycloak OIDC service. KYPO CRP supports with Keycloak:

* local Keycloak users
* [external Kerberos and LDAP users](https://www.keycloak.org/docs/latest/server_admin/#_user-storage-federation)
* [external Identity Providers](https://www.keycloak.org/docs/latest/server_admin/#_identity_broker)

Using OIDC providers directly in KYPO CRP instead of local Keycloak service is still possible, but it's not recommended. The implementation might not be fully compatible with KYPO CRP. For the direct implementation of external service instead of local Keycloak service, continue with [General Setup](#general-setup) section.

## General Setup

Regardless of the used OIDC provider, you must register a new **Client** to obtain `client_id`.

!!! warning
    Make sure that OIDC provider:

    * Uses **JSON Web Token (JWT)** access tokens. Opaque tokens are not supported by the KYPO platform.

    * Supports the **user info endpoint** to validate the access token and retrieve base info about a user.


Set up the following parameters with given values.

1. Redirect URI

    ```
    https://<YOUR-SERVER-ADDRESS>
    https://<YOUR-SERVER-ADDRESS>/index.html
    https://<YOUR-SERVER-ADDRESS>/silent-refresh.html
    ```

2. Scopes
    * openid
    * profile
    * email

3. Grant Type
    * implicit

4. Response Types
    * token
    * id_token

5. Post-Logout Redirect

    ```
    https://<YOUR-SERVER-ADDRESS>/logout-confirmed
    ```

### Selecting the Right Grant Types
The selection of the right grant type is especially important for security reasons. In OpenID Connect exists 4 grant types:

1. Authorization code grant
2. Implicit code grant
3. Resource owner password credentials grant
4. Client credentials grant

Each type was predesigned for a different type of applications (**web, user-agent, native**), where web means web application that contains back-end, e.g., Spring MVC using JSP, user-agent represents just browser web apps as is Angular or React, and native represents desktop or mobile applications. Here:

* **Authorization code grant** was mainly developed for a web application where the client_id and client_secret are safely stored in the back-end part of the application.

* **Implicit code grant** was designed for user-agent applications that could not save client_secret in the code since it is directly propagated to the user in HTML. For that reason, we had used the Implicit code grant in our OIDC settings tutorial.

Currently, the **best practice for security reasons** in user-agent applications is to use the Authorization code grant + PKCE. This is perfectly described in the following [**RFC 7636**](https://tools.ietf.org/html/rfc7636).
