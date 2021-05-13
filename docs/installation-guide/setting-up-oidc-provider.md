# Setting up OIDC Provider (Local issuer)
    
This setup is done automatically by creating our CSIRT-MU dummy OIDC issuer in KYPO CRP Deployment installation guide.

## Manual setup of Relying Party and Resource Server in OIDC Provider

1. Open the webpage `https://<YOUR-SERVER-ADDRESS>/csirtmu-dummy-issuer-server`, and log in with credentials\
set up in your [extra-vars.yml]({{ page.meta.extra_vars_url }}) file as sub-variables **sub** and **password** in variable **kypo_crp_users**.
2. Click on "**Self-service Client Registration**" -> "**New Client**".
3. Set the Client name, e.g. `KYPO PROD/Devel Client`.
4. Add at least one custom Redirect URI. For example: 
    ```
    https://<YOUR-SERVER-ADDRESS>
    https://<YOUR-SERVER-ADDRESS>/index.html
    https://<YOUR-SERVER-ADDRESS>/silent-refresh.html
    ```

5. In tab "**Access**":
    1. choose which information about the user you will be getting, so-called `scopes`.
    2. select just *implicit* in **Grand Types**
    3. select *token* and *code id_token* in **Responses Types**
6. In the tab "**Other**" add **Post-Logout Redirects**, e.g. `https://<YOUR-SERVER-ADDRESS>/logout-confirmed`

7. Hit the **Save** button.
8. Then got to tab "**JSON**", copy the JSON file and save it to file. <u>**IMPORTANT STEP**</u>
9. Now create a new Resource in "**Self-service Protected Resource Registration**".
10. Again insert client Name and save JSON to an external file in the "**JSON**" tab.
11. In the tab "**Access**" again choose which information about the user you will be getting, so-called `scopes`.
12. Hit **Save** button.

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
