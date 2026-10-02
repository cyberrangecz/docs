Topology Definition is used for the description of [Topology Instance](topology-instance.md). See the following image to help you visualize what you can define in the topology definition.

![topology-definition-color](/img/user-guide-advanced/sandboxes/topology-definition-color.png){: .center style="max-height: 400px;" }

## Attributes

Attributes of a Topology Definition (an [example](#example)).

### name

Defines the name of the definition ([name restrictions](#names)).

### hosts

Hosts contains the list of end hosts to be deployed. A host has the following attributes.

* **name**: name of end host VM ([names restriction](#names), [unique names restriction](#unique-names))
* **flavor**: name of flavor (see [how to chose flavor](#flavor))
* **base_box**: (see [how to define base_box](#base_box))
    * **image**: name of image
    * **mgmt_user**: name of user with sudo privileges
    * **mgmt_protocol (optional)**: protocol used for communication with base_box instance. supported options are `ssh` and `winrm` (default: `ssh`)
    * **mgmt_password (optional)**: SSH password for images that cannot receive the injected management key (see [mgmt_password](#mgmt_password))
* **hidden (optional)**: whether the host should be hidden in a topology visualization (default: `False`)
* **managed (optional)**: whether the [stage one](#managed-hosts) of the provisioning configures the host (default: `True`, see [managed hosts](#managed-hosts))
* **volumes (optional)**: list of volumes that will be provisioned on the host (see [volumes](#volumes))
* **extra (optional)**: a map used for defining extra values for the host, has no additional effect.

#### volumes

*(Since sandbox-service 4.0.0 for `image`, required `size`, and the limits below)*

The list of disks of the host. Each volume has the following attributes.

* **size**: volume size in GB, required, at least `1`.
* **image (optional)**: image the volume is created from. The volume is blank when it is not set. The meaning depends on the cloud provider:
    * OpenStack: name of a Glance image.
    * AWS: ID of an EBS snapshot (`snap-...`).

The following rules apply.

* The first volume (`volumes[0]`) is the system disk. It is always created from `base_box.image`, so `image` cannot be set on it. The author of the definition has to determine how much space the image itself requires to run.
* A host can have at most 12 volumes.
* A volume cannot be smaller than the minimum disk size of the image it is created from. On OpenStack, this is the `min_disk` of the Glance image of `base_box.image` for `volumes[0]` and of `image` for the other volumes. On AWS, `volumes[0]` cannot be smaller than the root volume of the AMI.
* Volume images on OpenStack must exist in Glance, which is checked when the sandbox definition is registered, when a pool is created, and when a sandbox is allocated.
* The image naming strategy of the deployment (`image_naming_strategy` in the sandbox-service configuration) rewrites `image` of the volumes the same way as `base_box.image`, on every cloud provider. On AWS, `image` is a snapshot ID, so the pattern must not match `ami-` and `snap-` IDs.
* On AWS, `volumes[0]` resizes the root device, and the other volumes are attached as EBS volumes from `/dev/sdf` onwards. Before sandbox-service 4.0.0, `volumes` was ignored on AWS.
* On AWS, `image` must be an EBS snapshot owned by the platform account. This is checked when the sandbox definition is registered, when a pool is created, and when a sandbox is allocated. The `size` of the volume cannot be smaller than the snapshot. The platform AWS user needs `ec2:DescribeSnapshots` for the check. Every snapshot of the account can be used by the authors of definitions, so use a dedicated AWS account for sandboxes.

```yaml
volumes:
  - size: 16
  - size: 2
  - size: 20
    image: forensic-evidence-disk
```

### routers

The list of routers. Routers are the only nodes through which hosts can communicate with the internet or hosts in networks connected to different Routers. Every router should be connected to some [networks](#networks). A connection can be achieved by [router_mappings](#router_mappings). A router has the following attributes.

* **name**: name of router VM ([names restriction](#names), [unique names restriction](#unique-names))
* **flavor**: name of flavor (see [how to chose flavor](#flavor))
* **base_box**: (see [how to define base_box](#base_box))
    * **image**: name of image
    * **mgmt_user**: name of user with sudo privileges
    * **mgmt_protocol (optional)**: protocol used for communication with base_box instance. supported options are `ssh` and `winrm` (default: `ssh`)
    * **mgmt_password (optional)**: SSH password for images that cannot receive the injected management key (see [mgmt_password](#mgmt_password))
* **extra (optional)**: a map used for defining extra values for the router, has no additional effect.
* **hidden (optional)**: whether the router and its networks and hosts should be hidden in a topology visualization (default: `False`)

    !!! note
        A router's **cidr** attribute has been deprecated since version 21.12.

### wan
A special network that [routers](#routers) uses to communicate with each other and the Internet. [Routers](#routers) are assigned to this network automatically.

* **name**: name of the network (default: `wan`, [names restriction](#names), [unique names restriction](#unique-names))
* **cidr**: IPv4 address range in CIDR notation (default: `100.100.100.0/24`, [unique cidrs restriction](#disjunct-cidrs))

### networks

The list of networks. A network is used to connect the router with the end host. It has the following attributes.

* **name**: name of network ([names restriction](#names), [unique names restriction](#unique-names))
* **cidr**: IPv4 address range in CIDR notation ([unique cidrs restriction](#disjunct-cidrs))
* **accessible_by_user**: optional attribute, specifies which networks will be accessible by user (default: `True`), applies to the all hosts of a network
* **hidden (optional)**: whether the network and its hosts should be hidden in a topology visualization (default: `False`)

### net_mappings

The list of net_mappings. A net_mapping is used to connect the host to the network. Each host should be connected to one network (more are possible but not recommended). A net_mapping has the following attributes.

* **host**: name of host defined in [hosts](#hosts)
* **network**: name of the network defined in [networks](#networks)
* **ip**: IPv4 address for the host, must be from IP address range of the network [address restriction](#address-restriction)

### router_mappings

The list of router_mappings. A router_mapping is used to connect the router to the network. Each network should be connected to one router, but one router can be connected to multiple networks. A router_mapping has the following attributes.

* **router**: name of router defined in [routers](#routers)
* **network**: name of network defined in [networks](#networks)
* **ip**: IPv4 address for the router, must be from IP address range of the network [address restriction](#address-restriction)

### groups

The list of groups. An ansible group is used for better management of nodes. It has the following attributes.

* **name**: name of the group
* **nodes**: list of node names defined in [hosts](#hosts), or [routers](#routers).

The following group names are reserved for monitoring - monitor-os (monitoring of Operating System), monitor-icmp (network availability monitoring on management interface).

### monitoring_targets

Definition of the targets to be monitored. It is split into three independent, optional sections: `tcp`, `icmp`, and `http`.

#### tcp

List of nodes with TCP ports to monitor. Each entry has the following attributes.

* **node**: name of host or router defined in [hosts](#hosts) or [routers](#routers). Each node may be listed only once.
* **targets**: list of TCP ports to monitor. Each target has the following attributes.
    * **port**: TCP port to monitor (`1`–`65535`).
    * **interface**: network interface to monitor. Exactly one of `interface` or `address` must be specified.
    * **address**: IP address or CIDR to monitor. Exactly one of `interface` or `address` must be specified.

The same port may be defined multiple times on a single node, as long as it targets different interfaces or addresses.

#### icmp

List of nodes whose ICMP (ping) availability should be monitored. Each entry has the following attributes.

* **node**: name of host or router defined in [hosts](#hosts) or [routers](#routers). Each node may be listed only once.
* **targets**: list of targets to monitor. Each target has the following attributes.
    * **interface**: network interface to monitor. Exactly one of `interface` or `address` must be specified.
    * **address**: IP address or CIDR to monitor. Exactly one of `interface` or `address` must be specified.

#### http

HTTP endpoints to monitor. Unlike `tcp` and `icmp`, these targets are not bound to a specific node.

* **targets**: list of endpoints to monitor. Each target has the following attributes.
    * **url**: endpoint to monitor. Must be a valid `http` or `https` URL.
    * **check_string**: optional string that must be present in the response body for the endpoint to be considered healthy.

```yaml
monitoring_targets:
  tcp:
    - node: server-router
      targets:
        - port: 22
          interface: ens3
        - port: 22
          address: 10.10.20.0/24
  icmp:
    - node: server
      targets:
        - interface: ens3
    - node: home
      targets:
        - address: 10.10.30.5
  http:
    targets:
      - url: https://10.10.20.5
        check_string: "Hello"
```

### vpn

*(Since CyberRangeCZ Platform v2026.07)*

Optional configuration that enables NetBird (WireGuard-based mesh) VPN access to the sandbox. When defined, selected nodes are enrolled as VPN gateways ("entrypoints"), so a VPN client can join the sandbox mesh and reach the declared internal networks directly. It has two independent, optional sections: `entrypoints` and `dns`.

#### entrypoints

List of [hosts](#hosts) or [routers](#routers) that act as VPN gateways. Each entrypoint is enrolled as a NetBird routing peer, and VPN clients reach the listed networks through it. Each entry has the following attributes.

* **name**: name of a host or router defined in [hosts](#hosts) or [routers](#routers). It must reference an existing node.
* **routes**: non-empty list of networks reachable through this entrypoint, in IPv4 CIDR notation (typically the sandbox internal networks to expose).

#### dns

Optional DNS settings distributed to every VPN client of the sandbox.

* **servers**: non-empty list of IPv4 nameserver addresses the clients should use.
* **search_domains (optional)**: list of DNS search domains. Each must be a valid domain name.

```yaml
vpn:
  entrypoints:
    - name: server
      routes:
        - 10.10.0.0/16
    - name: server-router
      routes:
        - 192.168.0.0/16
  dns:
    servers:
      - 10.10.20.5
    search_domains:
      - sandbox.local
```

### network_forwarding

*(Since sandbox-service 4.0.0)*

Optional network traffic forwarding (port mirroring). A copy of the traffic on one or more source interfaces is delivered to a single destination interface, for example to a host running a traffic analysis tool. The definition can declare at most one rule.

* **sources**: non-empty list of the interfaces to mirror. The interfaces must be unique. Each source has the following attributes.
    * **node**: name of a host or router defined in [hosts](#hosts) or [routers](#routers).
    * **network**: name of the network defined in [networks](#networks) that the node is connected to.
* **destination**: the interface that receives the copy of the traffic. It has the same attributes as a source (`node` and `network`), and it cannot also be one of the sources.
* **direction (optional)**: which traffic is mirrored, relative to the source. One of `in`, `out`, and `both` (default: `both`).

The interfaces are referenced by node and network, so each of them has to exist in [net_mappings](#net_mappings) or [router_mappings](#router_mappings), and only once: a node with two interfaces on the same network cannot be a source or the destination. The rule is validated after the whole definition is loaded, so its position in the file does not matter.

Example for OpenStack. The sources are on `server-switch` and the destination is on the separate network `mirror-switch`.

```yaml
network_forwarding:
  sources:
    - node: server
      network: server-switch
    - node: server-router
      network: server-switch
  destination:
    node: analyzer
    network: mirror-switch
  direction: both
```

Example for AWS. Every source is on the network of the destination, so `analyzer` is connected to `server-switch` as well.

```yaml
network_forwarding:
  sources:
    - node: server
      network: server-switch
    - node: server-router
      network: server-switch
  destination:
    node: analyzer
    network: server-switch
  direction: both
```

Network forwarding is available only when the administrator of the platform turns it on (`network_forwarding_enabled` in the sandbox-service configuration). Otherwise, a definition with `network_forwarding` is rejected when it is imported, when a pool is created, and when a sandbox is allocated. The rules differ per cloud provider.

#### OpenStack

The platform uses Neutron TaaS (with the OVN driver) to mirror the traffic and delivers it to the destination encapsulated in GRE. See the [OpenStack requirements](../../installation-guide/openstack-requirements.md#network-forwarding) for the prerequisites.

* The destination is a host (not a router) that has another interface in a user network. It uses that interface for its sandbox traffic.
* No other host is connected to the destination network. The network carries only the mirrored traffic, and nothing on it can send traffic. The topology router of the network is allowed.
* A TCP or ICMP [monitoring target](#monitoring_targets) of the destination cannot be an `address` inside the destination network, and no HTTP monitoring target can be a URL whose host is an IP address inside the destination network.
* The copy is delivered to the destination as GRE packets, and there is no return route towards the mirroring hypervisors, so the destination should capture the traffic rather than reply to it.
* A sandbox with network forwarding uses additional resources of the OpenStack project, see [quotas](../../installation-guide/openstack-requirements.md#network-forwarding).

#### AWS

The platform uses VPC Traffic Mirroring.

* Every source is on the network of the destination. Each network is its own VPC, and the traffic cannot be mirrored across VPCs.
* There are at most 10 sources.
* The instance type (`flavor`) of the sources is from the `t3`, `t3a`, or `t4g` family. Other types, such as `t2`, do not support Traffic Mirroring.
* The destination receives the traffic as VXLAN on UDP port 4789. The VXLAN network identifier (VNI) is assigned by AWS.
* The AWS user of the platform needs the EC2 Traffic Mirroring permissions (for the mirror target, filter, filter rule, and session), as listed in the [IAM policy of devops-tf-deployment](https://github.com/cyberrangecz/devops-tf-deployment/blob/master/tf-aws-base/IAM-EC2.md).

!!! warning
    The OpenStack and AWS rules conflict (for example, the OpenStack destination network cannot contain other hosts, while the AWS sources have to be on it), so in practice a useful forwarding definition is valid on only one of the two cloud providers.

## Glossary

### Base_box

Base_box specifies the `image` of the node boot disk, default user `mgmt_user` with sudo permissions, and a protocol that is needed to communicate with the machine.

The table below contains some examples of possible base_box options.

| image                | user    |
|----------------------|---------|
| centos-8             | centos  |
| cirros-0-x86_64      | cirros  |
| debian-12-x86_64     | debian  |
| kali-2020.4          | debian  |
| ubuntu-noble-x86_64  | ubuntu  |
| windows-10           | windows |
| windows-server-2019  | windows |

!!! warning
    The actual base_box options may differ from the contents of this table. Before using an image, check that it is present in the list of OpenStack images ([How to list OpenStack images](../../installation-guide/installation-guide-overview.md#configuration))

!!! note
    It is strongly recommended to use the `debian-12-x86_64` or `ubuntu-noble-x86_64` images for routers.


#### mgmt_password

*(Since sandbox-service 4.0.0)*

Some images cannot receive the management SSH key the platform injects into the instance (for example, a network appliance). For them, `mgmt_password` provides an SSH password.

```yaml
base_box:
  image: appliance-image
  mgmt_user: admin
  mgmt_password: changeme
```

* It is supported only with `mgmt_protocol: ssh`, for hosts and routers.
* It must not be empty.
* The injected management key is tried first, and the password is used as a fallback.
* The inventory contains the password as `ansible_password` and also as `ansible_become_password`, so it is used as the `sudo` password too.
* The Ansible runner image has to contain `sshpass`. Use the Ansible runner image `crczp-ansible-runner` 1.2.0 or newer.

!!! warning
    The password is stored in plaintext in the sandbox definition repository and on the platform. SSH host keys are not verified during the provisioning. Use only the default password of an image or a throwaway credential.

### Flavor

Flavor defines virtual machine hardware parameters (VCPUs, RAM, Disk size).

The following flavors can be deployed using the CyberRangeCZ Platform deployment tools.

!!! warning
    In the case of using a public cloud provider (flavors cannot be created without admin rights), the flavors in the topology definition must be replaced by the available flavors of that provider.

[How to list OpenStack flavors](../../installation-guide/installation-guide-overview.md#configuration)

| flavor          | vCPU | RAM (GB) | disk size (GB) |
|-----------------|------|----------|----------------|
| standard.small  | 1    | 2        | 80             |
| standard.medium | 1    | 4        | 80             |
| standard.large  | 2    | 16       | 80             |


### Managed hosts

*(Since sandbox-service 4.0.0)*

The host attribute `managed` (default: `True`) controls whether the stage one of the provisioning configures the host. When it is `False`, the stage one never configures the host: networking, hostname, user access, Docker, NetBird, and monitoring exporters are all left alone. The host is still created, connected to its networks, and part of the Ansible inventory, so the `playbook.yml` of the [Sandbox Provisioning](sandbox-provisioning.md) can configure it. It is intended for appliances and other images that the platform cannot configure.

Routers carry the sandbox routing, so they are always managed and have no `managed` attribute. Hosts with `managed: False` belong to the `unmanaged_hosts` [Ansible host group](sandbox-provisioning.md#ansible-host-groups), whose name is reserved.

The following is rejected for an unmanaged host.

* A TCP or ICMP target in [monitoring_targets](#monitoring_targets), because the stage one never gathers the facts of the host.
* A [vpn](#vpn) entrypoint, because the NetBird agent is never installed on the host.
* A container mapping of [Docker containers](sandbox_dockers.md), because Docker is never installed on the host.

An unmanaged host can be a [network_forwarding](#network_forwarding) destination and can be connected to user-accessible networks.

!!! note
    Unmanaged hosts require a version of the Ansible stage one repository newer than v2.2.1 (v2.3.0 or later).

## Restrictions

### Names

All names should have only characters: `a-z`, `A-Z`, `1-9`, and `-`, and the first character should be a lower case letter.

### Unique Names

Names of hosts, networks, and routers should be unique in the context of a Topology Definition (they are used for instance identification). The names `man` and `man-network` are reserved for the management node and network.

### Disjunct CIDRs

Networks, including wan, should be disjunct (not overlapping), and in `network_mappings` and `router_mappings` IP address should be from the IP address range of the network. Otherwise, networking wouldn't work.
Networks, including wan, shouldn't overlap with [management network's](topology-instance.md#topology-instance-management) CIDR either.

### Address Restriction

During a network creation, the OpenStack will take the first IP address of the specified IP address range for a gateway (a Router), the second IP address for DHCP, and the rest for hosts. The OpenStack will non-deterministically take the first address of the network or the first address after a gateway (a Router) address, and if any of net_mappings has an IP address set to one of these addresses, sandbox creation may fail.

### Group Restriction

Sandbox service does not allow the redefinition of its [default hosts groups](sandbox-provisioning.md#ansible-host-groups). Thus, the Topology Definition in which these groups are defined is invalid.

*[VM]: Virtual machine
*[BR]: Border router
*[UAN]: User Access Node
## Example

An example topology definition in the sandbox definition with the name `small-sandbox` contains the following.

* Two hosts. The host server will not be visible in the topology.
* Two routers.
* The wan network with a custom name.
* Two networks. Only one is user-accessible and therefore connected to the UAN node.
* One group, which contains two nodes.

```yaml
name: small-sandbox
hosts:
  - name: server
    base_box:
      image: debian-12-x86_64
      mgmt_user: debian
    flavor: standard.small
    hidden: True
    volumes:
      - size: 16
      - size: 2
      - size: 9

  - name: home
    base_box:
      image: windows-10-0.2.0
      mgmt_user: windows
      mgmt_protocol: wirm
    flavor: standard.small

routers:
  - name: server-router
    base_box:
      image: debian-12-x86_64
      mgmt_user: debian
    flavor: standard.small

  - name: home-router
    base_box:
      image: debian-12-x86_64
      mgmt_user: debian
    flavor: standard.small

wan:
  name: internet-connection
  cidr: 100.100.100.0/24

networks:
  - name: server-switch
    cidr: 10.10.20.0/24
    accessible_by_user: False

  - name: home-switch
    cidr: 10.10.30.0/24

net_mappings:
    - host: server
      network: server-switch
      ip: 10.10.20.5

    - host: home
      network: home-switch
      ip: 10.10.30.5

router_mappings:
    - router: server-router
      network: server-switch
      ip: 10.10.20.1

    - router: home-router
      network: home-switch
      ip: 10.10.30.1

groups:
  - name: custom-group
    nodes:
      - home
      - home-router
```
