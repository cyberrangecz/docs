As mentioned before, the KYPO platform is used to create and provide an emulated environment. Working with the emulated environment in KYPO requires knowledge of the following terms:

* [**Sandbox**](#sandbox)
* [**Sandbox definition**](#sandbox-definition)
* [**Pool**](#pool)

## Sandbox
An emulated environment is also called a sandbox. It is an isolated testing environment that enables users to run programs or execute files without affecting the application, system, or platform on which they run. In the context of KYPO, a sandbox is the virtual network infrastructure created using the OpenStack cloud service that consists of virtual machines and virtual networks.

## Sandbox Definition
The creation of the sandbox requires the definition of the sandbox structure and configuration of the individual virtual machines. The definition in the context of KYPO is the directory named after sandbox definition which contains: 

* **Topology Definition**: The file with the sandbox structure definition (hosts, routers, networks, etc.). For more detailed information about the topology definition, check the page [Toplogy Definition](../sandbox-topology/topology-definition). Created sandbox inside the cloud is called KYPO [Topology Instance](../sandbox-topology/topology-instance).
* **Sandbox Provisioning**: It is used to customize Topology Instances, e.g., set up environment, create users, install packages, etc. Sandbox Provisioning must specify the way how to connect to instances, e.g., user name and SSH key. The Ansible tool is used to perform these actions. For more detailed information about the topology definition, check the page [Sandbox Provisioning](../sandbox-provisioning).

Created sandbox definitions must be stored as a GIT repository so it can be used inside the KYPO portal. GIT repository also must be accessible by the KYPO platform. For more detailed information about the topology definition, check the page [Sandbox Definition](../sandbox-definition).

## Pool
Before creating sandboxes, it is essential to create in system so-called pools. Pools are groups of sandboxes that are created based on the same sandbox definition. A definition is specified before creating the pool. After creating the pool, it is possible to start with the allocation of the sandboxes, which is divided into three phases:
    
1. **Sandbox Allocation**: The creation of sandbox (virtual machines) inside the cloud.
2. **Sandbox Networking**: Networking of the virtual machines and user keys distribution to machines. The phase is executed automatically and is not the responsibility of the user. 
3. **Sandbox Provisioning**: Customization of virtual machines already above-mentioned. 
 

![kypo-basic-elements-sandboxes](/img/operation-guide/sandboxes/KYPO-basic-elements-sandboxes.png)
