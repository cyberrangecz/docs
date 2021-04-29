The Sandbox Provisioning is for [Topology Instance](../topology-instance/) customizations. Use it to set up your environment, create users, install packages, etc.

The **provisioning** directory's content is the same as any other [Ansible](https://docs.ansible.com/ansible/latest/index.html).

* **playbook.yml**: the Ansible playbook that is used for provisioning of the sandbox,
see Ansible documentation on [playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html).
* **pre-playbook.yml (optional)**: the Ansible playbook that is expected to be used to install packages necessary for **playbook.yml**.
* **requirements.yml (optional)**: the Ansible Galaxy requirements file that contains Ansible role dependencies, see Ansible documentation on [installing roles from a file](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-multiple-roles-from-a-file).
* **roles (optional)**: the directory for Ansible roles, see Ansible documentation on [roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html).
* **group_vars (optional)**: the directory for group variables, see Ansible documentation [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).
* **host_vars (optional)**: the directory for host variables, see Ansible documentation on [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).

### Minimal Ansible Playbook

The KYPO requires Sandbox Provisioning, but if you do not need any provisioning, you can use a dummy `playbook.yml` file containing only the following line.

```yaml
- hosts: all
```

### Ansible Host Groups

On top of [default Ansible host groups](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#default-groups), the KYPO sandbox-service defines three more default host groups.

* **management**: the group containing all the [sandbox management nodes](../topology-instance/#topology-instance-management), i.e., MAN, BR, and UAN node.
* **routers**: the group containing all the routers defined in [Topology definition](../topology-definition/#routers).
* **hosts**: the group containing all the hosts defined in [Topology definition](../topology-definition/#hosts).

You can specify additional Ansible host groups in [Topology definition](../topology-definition/#groups) and then use them in a `playbook.yml` file of the Sandbox Provisioning.

### Ansible Special Variables

On top of [Ansible special variables](https://docs.ansible.com/ansible/latest/reference_appendices/special_variables.html), the KYPO sandbox-service defines more special variables.

* **kypo_global_openstack_stack_id**: the ID of sandbox representation in OpenStack cloud.
* **kypo_global_pool_id**: the ID of the pool for which the sandbox was created.
* **kypo_global_sandbox_allocation_unit_id**: the ID of the sandbox allocation unit. Once the sandbox is fully provisioned, it is the same ID as the sandbox ID.
* **kypo_global_sandbox_ip**: the sandbox IPv4 address.
* **kypo_global_sandbox_name**: the sandbox name, which is the compound of [stack_name_prefix](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/extra-vars.yml), pool ID and sandbox allocation unit ID.
* **kypo_global_head_ip**: the KYPO head server IP address.

### Ansible Inventory

For each sandbox, the KYPO sandbox-service generates an `inventory.yml` file. It adds some networking data to it, which you might find useful in your Sandbox Provisioning.

Example of inventory file for [small-sandbox](../topology-definition#example) defined in [Topology definition](../topology-definition) example.

```yaml
all:
  hosts:
    home:
      ansible_host: 192.168.128.5
      ansible_user: windows
    server:
      ansible_host: 192.168.128.4
      ansible_user: debian
    border-router:
      ansible_host: 192.168.128.3
      ansible_user: kypo-man
      interfaces:
        - def_gw_ip: 192.168.0.2
          mac: 00:00:00:00:00:07
          routes: []
        - def_gw_ip: null
          mac: 00:00:00:00:00:14
          routes:
            - gw: 100.100.100.3
              mask: 255.255.255.0
              net: 10.10.20.0
        - def_gw_ip: null
          mac: 00:00:00:00:00:17
          routes:
            - gw: 200.100.100.2
              mask: 255.255.255.0
              net: 10.10.30.0
      ip_forward: true
    man:
      ansible_host: 10.10.10.10
      ansible_user: kypo-man
      interfaces:
        - def_gw_ip: null
          mac: 00:00:00:00:00:02
          routes: []
        - def_gw_ip: null
          mac: 00:00:00:00:00:03
          routes:
            - gw: 192.168.0.1
              mask: 255.255.255.248
              net: 100.100.100.0
            - gw: 192.168.0.1
              mask: 255.255.255.0
              net: 10.10.20.0
            - gw: 192.168.0.1
              mask: 255.255.255.248
              net: 200.100.100.0
            - gw: 192.168.0.1
              mask: 255.255.255.0
              net: 10.10.30.0
      ip_forward: true
      user_private_key_path: /root/.ssh/user_key
      user_public_key_path: /root/.ssh/user_key.pub
    uan:
      ansible_host: 192.168.128.2
      ansible_user: kypo-man
      interfaces:
        - def_gw_ip: 192.168.0.17
          mac: 00:00:00:00:00:05
          routes: []
    home-router:
      ansible_host: 192.168.128.7
      ansible_user: debian
      interfaces:
        - def_gw_ip: 200.100.100.3
          mac: 00:00:00:00:00:16
          routes: []
      ip_forward: true
    server-router:
      ansible_host: 192.168.128.6
      ansible_user: debian
      interfaces:
        - def_gw_ip: 100.100.100.3
          mac: 00:00:00:00:00:13
          routes: []
      ip_forward: true
    kypo_proxy_jump:
      ansible_host: jump-host-ip
      ansible_user: debian
  children:
    hosts:
      hosts:
        home: null
        server: null
    management:
      hosts:
        man: null
        uan: null
        border-router: null
    routers:
      hosts:
        home-router: null
        server-router: null
    user-accessible:
      hosts:
        home: null
        home-router: null
    winrm_nodes:
      hosts:
        home:
      vars:
        ansible_connection: psrp
        ansible_psrp_auth: certificate
        ansible_psrp_cert_validation: ignore
        ansible_psrp_certificate_key_pem: /root/.ssh/pool_mng_key
        ansible_psrp_certificate_pem: /root/.ssh/pool_mng_cert
        ansible_psrp_proxy: 'socks5://localhost:12345'
    ssh_nodes:
      hosts:
        server:
        home-router:
        server-router:
  vars:
    kypo_global_head_ip: 0.0.0.0
    kypo_global_openstack_stack_id: heatstack-stack-id
    kypo_global_pool_id: 1
    kypo_global_sandbox_allocation_unit_id: 1
    kypo_global_sandbox_ip: 10.10.10.10
    kypo_global_sandbox_jump_host: 'absent'
    kypo_global_sandbox_name: stack-name
```
