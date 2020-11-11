# Overview

This guide contains the steps that are needed to prepare the KYPO Cyber Range Platform (KYPO CRP) for cyber exercises and the creation of emulated virtual environments. It is divided into 3 major sections:

* [OpenStack Requirements](../openstack-requirements) describes a configuration that is required by the KYPO CRP from the OpenStack cloud platform.

* [Base Infrastructure](../base-infrastructure) contains steps that will help you to create all the necessary objects within the OpenStack cloud platform for the KYPO CRP to run. It mainly consists of 2 servers and a network.
    * **KYPO Head**: The server where the KYPO CRP is installed.
    * **KYPO Proxy**: The server used only for SSH access to all sandboxes.
    * **KYPO Base Network**: The network where both servers and all sandboxes are connected.
    
    ![base-infrastructure](../../img/installation-guide/base-infrastructure.png)
    
* [KYPO CRP Deployment](../kypo-crp-deployment) contains steps that will help you to create configuration files used by Ansible to install and configure the KYPO CRP on the KYPO Head server in the OpenStack cloud platform.
