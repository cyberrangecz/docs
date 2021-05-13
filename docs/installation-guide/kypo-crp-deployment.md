---
extra_vars_url: https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/extra-vars.yml
secrets_url: https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/secrets.yml
obtain_application_credentials_url: https://docs.openstack.org/keystone/ussuri/user/application_credentials.html
base_infrastructure_url: ../base-infrastructure
setting_up_oidc_provider_url: ../setting-up-oidc-provider
administration_agenda_url: ../../user-guide-basic/administration-agenda/administration-agenda-overview
---

# KYPO CRP Deployment

This page contains the steps that are needed to install and configure the KYPO Cyber Range Platform. You can clone the [KYPO CRP Deployment Repository](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment) via the following command.

```shell
git clone https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment.git
```

## Prerequisites

Install the following technology:

Technology      | Installation                               | Version
----------      | ---------------                            | -------
Ansible         | `apt install ansible`                      | 2.10.5+
python3-passlib | `apt install python3-passlib`              | 1.7+
bcrypt          | `pip3 install bcrypt`                      | 3.2+

## Configure

1. Configure access to the OpenStack cloud.

    1. [Obtain Application Credentials]({{ page.meta.obtain_application_credentials_url }}).

    2. Edit the following variables of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using values obtained from the previous step.

        ```yaml
        # The URL of OpenStack Identity service API.
        kypo_crp_os_auth_url: <OS_AUTH_URL>
        # The ID of application credentials to authenticate at the OpenStack cloud platform.
        kypo_crp_os_application_credential_id: <OS_APPLICATION_CREDENTIAL_ID>
        # The secret string of `kypo_crp_os_application_credential_id`.
        kypo_crp_os_application_credential_secret: <OS_APPLICATION_CREDENTIAL_SECRET>
        ```

2. Configure access to the KYPO CRP Proxy machine that has direct access to the virtual network dedicated to sandboxes.

    1. Obtain access to the VM from [Base Infrastructure]({{ page.meta.base_infrastructure_url }}), i.e.:

        * hostname
        * username
        * passwordless SSH key

        And make sure you can access it.

        ```shell
        ssh -i <passwordless-ssh-key> <username>@<hostname>
        ```

    2. Edit the following variables of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using values obtained from the previous step.

        ```yaml
        # The KYPO Jump host IP address or hostname.
        kypo_crp_proxy_host: <hostname>
        # The name of the user on the KYPO Jump host.
        kypo_crp_proxy_user: <username>
        ```

    3. Encode the obtained passwordless SSH key using the base64 tool.

        ```shell
        base64 <passwordless-ssh-key>
        ```

    4. Edit the following variable of an [secrets.yml]({{ page.meta.secrets_url }}) file using value obtained from the previous step.

        ```yaml
        # The base64 encoded content of private SSL key used for communication with `kypo_crp_proxy_host`.
        kypo_crp_proxy_key: |-
            <encoded-passwordless-ssh-key
            spanning-multiple-lines>
        ```

3. Configure access to the KYPO CRP Head machine.

    1. Obtain access to the VM from [Base Infrastructure]({{ page.meta.base_infrastructure_url }}), i.e.:

        * hostname
        * username
        * SSH key

        And make sure you can access it.

        ```shell
        ssh -i <passwordless-ssh-key> <username>@<hostname>
        ```

    2. Edit the following variable of an inventory.ini file using value obtained from the previous step.

        ```ini
        [kypo_head]
        kypo
        [kypo_head:vars]
        ansible_host=<hostname>
        ansible_user=<username>
        ansible_ssh_private_key_file=<ssh-key>
        ```

    3. Edit the following variable of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using value obtained from the previous step.

        ```yaml
        # The FQDN or IP address of KYPO CRP.
        kypo_crp_host: <hostname>
        ```

4. Configure an SSL certificate that will be used for HTTPS communication.

    1. Obtain a certificate either from your Certification Authority (CA) or generate a self-signed one e.g. with command bellow.
        ```shell
        openssl req -newkey rsa:4096 -x509 -sha256 -days 3650 -nodes -out kypo.crt -keyout kypo.key -subj "/C=AU/ST=Some-State/O=Internet Widgits Pty Ltd/CN=x.x.x.x 
        ```
        Where CN is IP address of your KYPO Head server.

    2. Encode obtained certificate and its key using the base64 tool.

        ```shell
        base64 <certificate.pem>
        base64 <certificate.key>
        ```

    3. Edit the following variables of an [secrets.yml]({{ page.meta.secrets_url }}) file using values obtained from the previous step.

        ```yaml
        # The base64 encoded content of SSL certificate that is used by KYPO CRP for HTTPS communication.
        kypo_crp_cert: |-
            <encoded-certificate.pem
            spanning-multiple-lines>
        # The base64 encoded content of private SSL key of `kypo_crp_cert`.
        kypo_crp_cert_key: |-
            <encoded-certificate.key
            spanning-multiple-lines>
        ```

5. Configure initial users.

    There has to be at least one initial user with admin permissions that will be able to manage other users. See [Administration Agenda]({{ page.meta.administration_agenda_url }}). Edit the following variables of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using your desired values.

    !!! info "CSIRT-MU dummy OIDC issuer"

        The format of variable `sub` is `<user-login>@oidc.csirt.muni.cz`
        The variable `iss` is `https://<kypo_crp_head>:8443/csirtmu-dummy-issuer-server/`

    ```yaml
    kypo_crp_users:
          # The unique identifier of the user within the OIDC provider.
        - sub: admin@example.com
          # The URL of the OIDC provider.
          iss: https://example.com:443/issuer/
          # A password of the user.
          password: password
          # An email address of the user.
          email: admin@example.com
          # The user full name.
          fullName: "Demo Admin"
          # The user given name.
          givenName: "Demo"
          # The user family name.
          familyName: "Admin"
          # The boolean value that represents whether the user is admin or not.
          admin: True
    ```

6. Configure OpenID Connect providers.

    1. There has to be at least one OIDC issuer defined. If you do not have one, you can create our CSIRT-MU dummy OIDC issuer.
        
        ```shell
        ansible-galaxy install -r provisioning/requirements.yml -p provisioning/roles_required
        ansible-playbook -i inventory.ini provisioning/docker.yml --extra-vars=@extra-vars.yml --extra-vars=@secrets.yml
        ansible-playbook -i inventory.ini provisioning-oidc/oidc.yml --extra-vars=@extra-vars.yml --extra-vars=@secrets.yml
        ```

        !!! warning "Security Risk"

            Do not use this issuer in the production environment, it could be a security risk.

        !!! info "CSIRT-MU dummy OIDC issuer"

            The issuer can be found at https://<kypo_crp_head\>:8443/csirtmu-dummy-issuer-server/

    2. Obtain OIDC URL and clients secrets from oidc-local-provider.yml file, which was auto-created after previous command.
        
        * url
        * client_id
        * resource_client_id
        * resource_client_secret
        
    3. Edit the following variables of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using values obtained from the previous step.

        ```yaml
        # The list of OIDC providers and their specification.
        kypo_crp_oidc_providers:
              # The label that is displayed as an option for authentication.
            - label: "Login with Example issuer"
              # The URL of resource server configuration.
              url: <url>
              # The ID of OIDC client.
              client_id: <client_id>
              # The ID of resource client.
              resource_client_id: <resource_client_id>
              # The secret for resource client `resource_client_id`.
              resource_client_secret: <resource_client_secret>
        ```

7. Configure access to the Gitlab repository.

    There has to be exactly one Gitlab specification. If you want to use KYPO CRP Internal Git, just leave the variable `kypo_crp_git` of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file set as follows.

    ```yaml
    kypo_crp_git: '{% raw %}{{ kypo_crp_git_internal }}{% endraw %}'
    ```

    !!! info "Optional"

        The rest of the Gitlab repository configuration is optional.

    1. Otherwise you will have to obtain the access information to an external Gitlab, i.e.:

        * hostname
        * REST API URL
        * passwordless SSH key - of the Gitlab user
        * access token - of the Gitlab user to be used for communication with REST API URL

    2. Encode obtained private and public SSH key using the base64 tool.

        ```shell
        base64 <passwordless-ssh-key>
        base64 <passwordless-ssh-key.pub>
        ```

    3. There has to be available [KYPO CRP Ansible Stage One](https://gitlab.ics.muni.cz/muni-kypo-crp/backend-python/ansible-networking-stage/kypo-ansible-stage-one) repository within your Gitlab, so you will have to fork it. Then obtain its **Clone with SSH** URL address and revision, i.e. branch, tag or commit SHA.

    4. Edit the following variables of an [extra-vars.yml]({{ page.meta.extra_vars_url }}) file using values obtained from the previous step.
        ```yaml
        # The Git repository settings.
        kypo_crp_git:
            # The type of Git repository. For external, keep the value set to GITLAB.
            type: GITLAB
            # The Git server hostname or IP address.
            server: <hostname>
            # The URL of Git REST server.
            rest_server_url: <rest-api-url>
            # The name of user used for communication with Git repository.
            user: git
            # The base64 encoded content of private SSL key that KYPO CRP uses to communicate with Git repository.
            private_key: |-
                <encoded-ssh-key
                spanning-multiple-lines>
            # The base64 encoded content of public part of `kypo_crp_git.private_key` SSL key.
            public_key: |-
                <encoded-ssh-key
                spanning-multiple-lines>
            # The access token for Git REST server.
            access_token: <access-token>
            # The URL of Ansible networking Git repository.
            ansible_networking_url: <kypo-crp-ansible-stage-one-url>
            # The revision of Ansible networking Git repository. Either branch name, tag, or SHA commit hash.
            ansible_networking_rev: <kypo-crp-ansible-stage-one-rev>
        ```

## Deploy    

Run the Ansible provisioning that will install and configure KYPO CRP.

```shell
ansible-playbook -i inventory.ini provisioning/docker.yml --extra-vars=@extra-vars.yml --extra-vars=@secrets.yml
ansible-playbook -i inventory.ini provisioning/playbook.yml --extra-vars=@extra-vars.yml --extra-vars=@secrets.yml
```
