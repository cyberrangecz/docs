The Sandbox Provisioning is for [Topology Instance](topology-instance.md) customizations. Use it to set up your environment, create users, install packages, etc.

The **provisioning** directory's content is the same as any other [Ansible](https://docs.ansible.com/ansible/latest/index.html).

* **playbook.yml**: the Ansible playbook that is used for provisioning of the sandbox,
see Ansible documentation on [playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html).
* **pre-playbook.yml (optional)**: the Ansible playbook that is expected to be used to install packages necessary for **playbook.yml**.
* **requirements.yml (optional)**: the Ansible Galaxy requirements file that contains Ansible role dependencies, see Ansible documentation on [installing roles from a file](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-multiple-roles-from-a-file).
* **roles (optional)**: the directory for Ansible roles, see Ansible documentation on [roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html).
* **group_vars (optional)**: the directory for group variables, see Ansible documentation [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).
* **host_vars (optional)**: the directory for host variables, see Ansible documentation on [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).

### Minimal Ansible Playbook

The CyberRangeCZ Platform requires Sandbox Provisioning, but if you do not need any provisioning, you can use a dummy `playbook.yml` file containing only the following line.

```yaml
- hosts: all
```

### Ansible Host Groups

On top of [default Ansible host groups](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#default-groups), the sandbox-service defines seven more default host groups.

* **management**: the group containing the [sandbox management node](topology-instance.md#topology-instance-management), i.e., MAN node.
* **routers**: the group containing all the routers defined in [Topology definition](topology-definition.md#routers).
* **hosts**: the group containing all the hosts defined in [Topology definition](topology-definition.md#hosts).
* **ssh_nodes**: the group containing all the hosts and routers defined in [Topology definition](topology-definition.md) with `base_box.mgmt_protocol` set to `SSH` (Since 21.04).
* **winrm_nodes**: the group containing all the hosts and routers defined in [Topology definition](topology-definition.md) with `base_box.mgmt_protocol` set to `WINRM` (Since 21.04).
* **user_accessible_nodes**: the group containing all hosts and routers defined in [Topology definition](topology-definition.md), which are connected to a network with attribute `accessible_by_user` set to `True` (Since 21.06).
* **hidden_hosts**: the group containing all hosts defined in [Topology definition](topology-definition.md) with attribute `hidden` set to `True` (Since 21.06).
* **windows_hosts**: the group containing all hosts defined in [Topology definition](topology-definition.md) with image os_type windows. This is parameter of image/ami in OpenStack/AWS cloud platform (Since CyberRangeCZ Platform v2025.01).

You can specify additional Ansible host groups in [Topology definition](topology-definition.md#groups) and then use them in a `playbook.yml` file of the Sandbox Provisioning.

### Ansible Special Variables

On top of [Ansible special variables](https://docs.ansible.com/ansible/latest/reference_appendices/special_variables.html), the sandbox-service defines more special variables.

* **global_openstack_stack_id**: the ID of sandbox representation in OpenStack cloud.
* **global_pool_id**: the ID of the pool for which the sandbox was created.
* **global_sandbox_id**: the UUID of the sandbox.
* **global_sandbox_allocation_unit_id**: the ID of the sandbox allocation unit. It is **not** the same as the sandbox UUID.
* **global_sandbox_ip**: the sandbox IPv4 address.
* **global_sandbox_name**: the sandbox name, which is the compound of [stackNamePrefix](https://github.com/cyberrangecz/devops-tf-deployment/blob/master/tf-head-services/values.yaml#L24), pool ID and sandbox allocation unit ID.
* **global_head_ip**: the CyberRangeCZ Platform IP address or FQDN.
* **global_ssh_public_user_key**: the path on Ansible controller to SSH public user key (Since 21.04).
* **global_ssh_public_mgmt_key**: the path on Ansible controller to SSH public management key (Since 21.04).
* **global_syslog_destination_port**: the Syslog destination port running on Kubernetes cluster (Since CyberRangeCZ Platform v2025.01).

### Ansible Inventory

For each sandbox, the sandbox-service generates an `inventory.yml` file. It adds some networking data to it, which you might find useful in your Sandbox Provisioning.

Example of inventory file for [small-sandbox](topology-definition.md#example) defined in [Topology definition](topology-definition.md) example.

```yaml
all:
  hosts:
    home:
      ansible_host: 192.168.128.3
      ansible_user: windows
      user_network_ip: 10.10.30.5
    home-router:
      ansible_host: 192.168.128.7
      ansible_user: debian
      interfaces:
      - def_gw_ip: 100.100.100.1
        mac: 00:00:00:00:00:16
        routes: []
      ip_forward: true
      user_network_ip: 10.10.30.1
    proxy-jump:
      ansible_host: jump-host-ip
      ansible_user: debian
      user_access_mgmt_name: pool-prefix
      user_access_present: true
      user_access_user_name: stack-name
    man:
      ansible_host: 10.10.10.10
      ansible_user: man
      interfaces:
      - def_gw_ip: ''
        mac: 00:00:00:00:00:02
        routes:
        - gw: 100.100.100.2
          mask: 255.255.255.0
          net: 10.10.20.0
        - gw: 100.100.100.3
          mask: 255.255.255.0
          net: 10.10.30.0
      ip_forward: true
    server:
      ansible_host: 192.168.128.2
      ansible_user: debian
      user_network_ip: 10.10.20.5
    server-router:
      ansible_host: 192.168.128.6
      ansible_user: debian
      interfaces:
      - def_gw_ip: 100.100.100.1
        mac: 00:00:00:00:00:13
        routes: []
      ip_forward: true
      user_network_ip: 10.10.20.1
  children:
    custom-group:
      hosts:
        home: null
        server-router: null
    hidden_hosts:
      hosts:
        server: null
    hosts:
      hosts:
        home: null
        server: null
    management:
      hosts:
        man: null
    routers:
      hosts:
        home-router: null
        server-router: null
    ssh_nodes:
      hosts:
        home-router: null
        server: null
        server-router: null
    user_accessible_nodes:
      hosts:
        home: null
        home-router: null
    winrm_nodes:
      hosts:
        home: null
      vars:
        ansible_connection: psrp
        ansible_psrp_auth: certificate
        ansible_psrp_cert_validation: ignore
        ansible_psrp_certificate_key_pem: /root/.ssh/pool_mng_key
        ansible_psrp_certificate_pem: /root/.ssh/pool_mng_cert
        ansible_psrp_proxy: socks5://localhost:12345
  vars:
    global_head_ip: 0.0.0.0
    global_openstack_stack_id: heatstack-stack-id
    global_pool_id: 1
    global_sandbox_allocation_unit_id: 1
    global_sandbox_ip: 10.10.10.10
    global_sandbox_name: stack-name
    global_ssh_public_mgmt_key: /root/.ssh/pool_mng_key.pub
    global_ssh_public_user_key: /root/.ssh/user_key.pub
```
