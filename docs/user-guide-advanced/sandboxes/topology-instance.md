# Topology Instance

The KYPO OpenStack Driver transforms a [Topology Definition](../topology-definition/) (user-defined topology) with the [Topology Instance Management](#topology-instance-management) sub-infrastructure into the HEAT Orchestration Template, which the OpenStack cloud platform uses to create a virtual infrastructure we call a KYPO Topology Instance.

![topology-instance-color](../../img/user-guide-advanced/sandboxes/topology-instance-color.png)

!!! note
    For clarity reasons, there are missing links from **man-network** to the left **Router** and left **Host**.

## Topology Instance Management

Every Topology Instance is created with management sub-infrastructure, which consists of the following.

* **MAN (Management Access Node)**: The only node connected to the network outside the Topology Instance. The network must be specified as a `base_network` in the [sandbox-service configuration](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/provisioning/roles/kypo-crp-head/templates/configuration/sandbox-service/kypo-sandbox-service-config.yml#L126). The Topology Instance is accessible only through the OpenStack cloud hypervisor or MAN.

* **man-network (management network)**: All nodes in the Topology Instance are connected to this network so that every node is accessible from `MAN` and can be configured through it. `CIDR` of this network should be specified in the configuration. The IP address range of this network can be overridden in the [sandbox-service configuration](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/provisioning/roles/kypo-crp-head/templates/configuration/sandbox-service/kypo-sandbox-service-config.yml#L138).
