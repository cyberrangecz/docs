The CyberRangeCZ Platform creates and provides an emulated virtual environment. Working with this environment in CyberRangeCZ Platform requires knowledge of the terms [Sandbox](#sandbox), [Sandbox definition](#sandbox-definition), and [Pool](#pool).

## Sandbox
As mentioned in [terminology](../../basic-concepts/terminology.md#emulated-virtual-environment), it is an isolated testing environment with virtual networks and virtual machines (VMs) in them. Thanks to the infrastructure created using the [OpenStack](https://www.openstack.org/) cloud service, and everything is running without affecting the external infrastructure.

## Sandbox Definition
As mentioned in [terminology](../../basic-concepts/terminology.md#emulated-virtual-environment), it is an isolated testing environment with virtual networks and virtual machines (VMs) in them. Thanks to the infrastructure created using the [OpenStack](https://www.openstack.org/) cloud service, and everything is running without affecting the external infrastructure.

* **Topology Definition**: The file with the sandbox structure definition (hosts, routers, networks, etc.). For more detailed information about the topology definition, check the page [Topology Definition](topology-definition.md). Created sandbox inside the cloud is called [Topology Instance](topology-instance.md).
* **Sandbox Provisioning**: It is used to customize Topology Instances, e.g., set up an environment, create users, install packages, etc. Sandbox Provisioning must specify how to connect to instances, e.g., user name and SSH key. The Ansible tool is used to perform these actions. For more detailed information about the topology definition, check the page [Sandbox Provisioning](sandbox-provisioning.md).

Created sandbox definition must be stored as a Git repository to be used inside the CyberRangeCZ Platform portal. Git repository must also be accessible by the CyberRangeCZ Platform. This means a GitLab repository with visibility set to public. Visiblity can also be private if the used CyberRangeCZ Platform instance has private access configured for the hosting git server.

For more detailed information, check the page [Sandbox Definition](sandbox-definition.md).

## Pool
Before creating cloud sandboxes, it is essential to create in system so-called pools. Pools are groups of sandboxes created based on the same sandbox definition. A definition is specified before creating the pool. After creating the pool, it is possible to start with the allocation of the sandboxes, which is divided into three phases:

1. **Sandbox Allocation**: Creating sandbox (virtual machines) inside the cloud.
2. **Sandbox Networking**: Networking of the virtual machines and user keys distribution to machines. The phase is executed automatically and is not the responsibility of the user.
3. **Sandbox Provisioning**: Customization of virtual machines already above-mentioned.


![basic-elements-sandboxes](/img/user-guide-advanced/sandboxes/basic-elements-sandboxes.svg){: .center style="max-height: 500px;"}
