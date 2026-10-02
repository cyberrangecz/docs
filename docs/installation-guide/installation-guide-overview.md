# Overview

!!! note
    If you want to deploy CyberRangeCZ Platform as a proof of concept to verify its usability for your project or create Training definitions for CyberRangeCZ Platform, consider using [CRCZP lite](https://github.com/cyberrangecz/devops-crczp-lite) deployment tool for easy zero-configuration deployment.

This guide contains the steps that are needed to prepare the CyberRangeCZ Platform for cyber exercises and the creation of emulated virtual environments.

Before the deployment, check the [OpenStack Requirements](openstack-requirements.md) section, which describes the requirements for the OpenStack cloud platform to be supported by CyberRangeCZ Platform.

If you meet the OpenStack Requirements follow with setting up the [Deployment Environment](https://github.com/cyberrangecz/devops-tf-deployment?tab=readme-ov-file#preparing-the-deployment-environment).

The deployment process is divided into 2 major sections:

* [Deployment of OpenStack base resources](https://github.com/cyberrangecz/devops-tf-deployment/blob/master/BASE.md) contains steps that will help you to create all the necessary objects within the OpenStack cloud platform for the CyberRangeCZ Platform to run. It deploys these resources:
    * **Kubernetes Cluster node**: The server running Kubernetes Controller & Worker services hosting the Head services.
    * **Proxy Jump**: The server used only for SSH access to all sandboxes.
    * **Base Network**: The network where both servers and all sandboxes are connected.
    * **Security Groups**: The firewall rules for all CyberRangeCZ Platform instances.
    * **CyberRangeCZ Platform Images**: The OpenStack images necessary for CyberRangeCZ Platform to work.
    * Optionally **Flavors**:  The OpenStack flavors necessary for CyberRangeCZ Platform to work. Only for OpenStack deployments with administrator credentials.

    ![Diagram of base infrastructure](/img/installation-guide/base-infrastructure.svg){: .center style="height: 500px;"}

* [Deployment of Helm application](https://github.com/cyberrangecz/devops-tf-deployment/blob/master/HELM.md) contains steps that will help you create configuration files and deploy CyberRangeCZ Platform with Helm to the Kubernetes Cluster node in the OpenStack cloud platform.

## Upgrading to sandbox-service 4.0.0

sandbox-service 4.0.0 changes the configuration and extends the topology definition. The Helm chart and the Terraform modules render the sandbox-service configuration, so use their releases listed below when you upgrade.

* **OpenStack options moved under `application_configuration.openstack`**: `auth_url`, `application_credential_id`, `application_credential_secret`, and `console_type` replace the flat `os_auth_url`, `os_application_credential_id`, `os_application_credential_secret`, and `os_console_type` keys. The service refuses to start when an old key is present, and the error names the new key.
* **`network_forwarding_enabled`**: new boolean option in `application_configuration` (default: `false`) that allows network forwarding.
* **Reserved Ansible group**: `unmanaged_hosts` is a reserved group name, so a [group](../user-guide-advanced/sandboxes/topology-definition.md#groups) of that name in a topology definition is rejected. Rename such a group in the definition **before** you upgrade: once the definition is read again, its existing pools and sandboxes stop working, not only new imports.
* **AWS volumes**: the [`volumes`](../user-guide-advanced/sandboxes/topology-definition.md#volumes) of a host were ignored on AWS before. They are honoured now: `volumes[0].size` resizes the root device, and the other volumes become billed EBS volumes. Check the sizes in existing definitions before you upgrade.
* **Helm values renamed**: the Helm chart 4.0.0 reads the OpenStack settings from `sandbox.openstack`. In your custom values, replace `sandbox.osAuthUrl`, `sandbox.osApplicationCredentialId`, `sandbox.osApplicationCredentialSecret`, and `sandbox.osConsoleType` with `sandbox.openstack.authUrl`, `sandbox.openstack.applicationCredentialId`, `sandbox.openstack.applicationCredentialSecret`, and `sandbox.openstack.consoleType`. The chart refuses to render when an old value is set.
* **tf-module-helm variables renamed**: in tf-module-helm v2.0.0, the variables `os_auth_url`, `application_credential_id`, and `application_credential_secret` are replaced by the single `openstack_config` variable (`authUrl`, `applicationCredentialId`, `applicationCredentialSecret`, and `consoleType`). Deployments made with devops-tf-deployment pass it on their own; set `os_console_type` there to change the console type.
* **`head_version`**: raise `head_version` to `4.0.0` in `deployment.tfvars` together with the bump to tf-module-helm v2.0.0. The module and the chart work only together, and the module rejects older versions.
* **Main interface of multi-homed nodes**: `user_network_ip` now follows the node's first [`net_mappings`](../user-guide-advanced/sandboxes/topology-definition.md#net_mappings) entry (for a router, its first `router_mappings` entry) instead of its last network in `networks:` order. Playbooks that read `user_network_ip` of other nodes, for example to write `/etc/hosts` aliases, get the new address, routers included. On Ubuntu and Debian 12+ hosts, the default route follows it too. Only nodes connected to more than one network are affected, and only in sandboxes allocated, or whose stages run, after the upgrade. A sandbox whose allocation is in progress during the upgrade, or whose failed user stage is restarted afterwards, can end up with the new `user_network_ip` but the old routes. The user SSH config of a multi-homed node now points to the main address first; this applies to existing sandboxes at once. To keep the old behaviour, move the mapping of that network to the top of the node's `net_mappings` (`router_mappings`), which also changes the order of its network interfaces. The console address and the AWS default route already used the first mapping.
* **Keycloak operator**: devops-tf-deployment installations from before this release also take the Keycloak operator switch of [tf-module-helm v1.9.0](https://github.com/cyberrangecz/tf-module-helm/tree/v1.9.0), which replaces the legacy Keycloak operator with the Hostzero Keycloak operator.
* **Components released together with the service**: the following versions or newer are needed for the new topology definition features.

| Component                | Version | Needed for                                                                      |
|--------------------------|---------|---------------------------------------------------------------------------------|
| sandbox-service          | 4.0.0   |                                                                                 |
| devops-helm (chart)      | 4.0.0   | configuration with the `openstack` section                                      |
| tf-module-helm           | v2.0.0  | configuration with the `openstack` section, `network_forwarding_enabled`        |
| tf-module-openstack-base | v1.3.0  | `sandbox-mirror-sg` and `base-router-public` for network forwarding             |
| ansible-stage-one        | v2.3.0  | `managed: false` hosts (any release newer than v2.2.1)                          |
| ansible-role-prometheus  | v2.0.2  | node exporter targets without unmanaged hosts                                   |
| backend-ansible-runner   | v1.2.0  | `base_box.mgmt_password` (image with `sshpass`)                                 |

The components are released in this order, because each one needs the previous ones: ansible-role-prometheus v2.0.2, ansible-stage-one v2.3.0, backend-ansible-runner v1.2.0, the sandbox-service 4.0.0 image, tf-module-openstack-base v1.3.0, the Helm chart 4.0.0, tf-module-helm v2.0.0, and devops-tf-deployment. To upgrade a deployment, apply tf-module-openstack-base v1.3.0 with `hypervisor_cidr` first, then tf-module-helm v2.0.0 with `head_version = "4.0.0"`, and turn on `network_forwarding_enabled` last.
