# Setting up OIDC Provider

Currently, the KYPO CRP is tested and supports the following OIDC providers: 

* [MUNI Unified Login](https://it.muni.cz/en/services/jednotne-prihlaseni-na-muni)
* [Microsoft Azure](https://azure.microsoft.com)
* [CSIRT-MU dummy OIDC issuer](https://gitlab.ics.muni.cz/csirt-mu-devel/oidc-auth/csirtmu-oidc-overlay)

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


## CSIRT-MU OIDC Dummy Issuer Setup
 

!!! info Automatic Setup 
    The setup is done automatically by creating our CSIRT-MU dummy OIDC issuer in the KYPO CRP Deployment installation guide.

1. Open the webpage `https://<YOUR-SERVER-ADDRESS>/csirtmu-dummy-issuer-server`, and log in with credentials set up in your [extra-vars.yml](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/extra-vars.yml) file as sub-variables **sub** and **password** in variable **kypo_crp_users**.
2. **Self-service Client Registration** > **New Client**
3. In the **Main** tab
    1. *Client name* - optional, e.g. *"KYPO PROD/Devel Client"*
    2. *Redirect URIs* 
        * `https://<YOUR-SERVER-ADDRESS>`
        * `https://<YOUR-SERVER-ADDRESS>/index.html`
        * `https://<YOUR-SERVER-ADDRESS>/silent-refresh.html`

4. In the **Access** tab select the following values
    1. *Scopes*
        * openid
        * profile
        * email 
    2. *Grant Types*
        * implicit
    3. *Responses Types*
        * token 
        * code id_token
6. In the **Other** tab 
    1. *Post-Logout Redirects* 
        * `https://<YOUR-SERVER-ADDRESS>/logout-confirmed`

7. Click the **Save** button.
8. In the **JSON** tab, copy the JSON file and save it to file. <u>**IMPORTANT STEP**</u>

### Required variables

!!! tip "CSIRT-MU dummy OIDC issuer"
        If you have created CSIRT-MU dummy OIDC issuer by following the KYPO CRP Deployment installation guide you can find the required variables in the auto-created *oidc-local-provider.yml* file.

The following variables are needed to deploy and use KYPO CRP with CSIRT-MU OIDC Dummy Issuer: 

* **client_id** - field `client_id` in the JSON file
* **url** - `https://<YOUR-SERVER-ADDRESS>/csirtmu-dummy-issuer-server/`

## Microsoft Azure Setup

1. Open and log in to the [Microsoft Azure portal](https://portal.azure.com/#home).
2. **Azure services** > **App registrations** > **New registration**
    1. *Name* - optional, e.g. *"KYPO PROD/Devel Client"*
    2. *Redirect URI*
        * Select *"Single-page application (SPA)"*
        * Add Redirect URI `https://<YOUR-SERVER-ADDRESS>`
3. Click the **Register** button
4. In the **Authentication** tab 
    1. *Single-page application* > *Redirect URIs*
        *  `https://<YOUR-SERVER-ADDRESS>`
        *  `https://<YOUR-SERVER-ADDRESS>/index.html`
        *  `https://<YOUR-SERVER-ADDRESS>/silent-refresh.html`
    2. *Front-channel logout URL*
        * `https://<YOUR-SERVER-ADDRESS>/logout-confirmed`
    3. *Implicit grant and hybrid flows*
        * Check *"Access tokens (used for implicit flows)"*
        * Check *"ID tokens (used for implicit and hybrid flows)"*
5. In the **API permissions** tab 
    1. *Add a permissions* > *Microsoft APIs* > *Microsoft Graph* > *Delegated permissions* > *OpenId permissions* 
        * openid
        * profile 
        * email
6. In the **Overview** tab 
    1. Save the value *"Application (client) ID"* 
    2. Save the value *"Directory (tenant) ID"*
    
### Required variables

The following variables are needed to deploy and use KYPO CRP with Microsoft Azure: 

* **client_id** - `Application (client) ID` (see the 6. step described above)
* **url** - `https://login.microsoftonline.com/<tenant ID>/v2.0/`
* **issuer_identifier** - `https://sts.windows.net/<tenant ID>/`
* **user_info_url** - `https://graph.microsoft.com/oidc/userinfo`


## Selecting the Right Grant Types
The selection of the right grant type is especially important for security reasons. In OpenID Connect exists 4 grant types:

1. Authorization code grant 
2. Implicit code grant
3. Resource owner password credentials grant
4. Client credentials grant

Each type was predesigned for a different type of applications (**web, user-agent, native**), where web means web application that contains back-end, e.g., Spring MVC using JSP, user-agent represents just browser web apps as is Angular or React, and native represents desktop or mobile applications. Here: 

* **Authorization code grant** was mainly developed for a web application where the client_id and client_secret are safely stored in the back-end part of the application.

* **Implicit code grant** was designed for user-agent applications that could not save client_secret in the code since it is directly propagated to the user in HTML. For that reason, we had used the Implicit code grant in our OIDC settings tutorial.

Currently, the **best practice for security reasons** in user-agent applications is to use the Authorization code grant + PKCE. This is perfectly described in the following [**RFC 7636**](https://tools.ietf.org/html/rfc7636).
