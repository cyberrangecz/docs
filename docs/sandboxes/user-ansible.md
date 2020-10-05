The User Ansible is for [Topology Instance](/sandboxes/sandbox-topology/topology-instance) customizations. Use it to set up your environment, create users, install packages, etc.

The content of the **provisioning** directory is the same as any other [Ansible](https://docs.ansible.com/ansible/latest/index.html).

* **playbook.yml**: the Ansible playbook that is used for provisioning of the sandbox,
see Ansible documentation on [playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html).
* **pre-playbook.yml (optional)**: the Ansible playbook that is expected to be used to install packages necessary for **playbook.yml**.
* **requirements.yml (optional)**: the Ansible Galaxy requirements file that contains Ansible role dependencies, see Ansible documentation on [installing roles from a file](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-multiple-roles-from-a-file).
* **roles (optional)**: the directory for Ansible roles, see Ansible documentation on [roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html).
* **group_vars (optional)**: the directory for group variables, see Ansible documentation [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).
* **host_vars (optional)**: the directory for host variables, see Ansible documentation on [host and group variables](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#organizing-host-and-group-variables).

### Minimal Ansible Playbook

The KYPO requires presence User Ansible, but if you do not need any provisioning, you can use a dummy `playbook.yml` file containing only the following line.

```yaml
- hosts: all
```

### Ansible Host Groups

On top of [default Ansible host groups](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#default-groups), the KYPO sandbox-service defines three more default host groups.

* **management**: the group containing all the [sandbox management nodes](/sandboxes/sandbox-topology/topology-instance#topology-instance-management), i.e., MAN, BR, and UAN node.
* **routers**: the group containing all the routers defined in [Topology definition](/sandboxes/sandbox-topology/topology-definition#routers).
* **hosts**: the group containing all the hosts defined in [Topology definition](/sandboxes/sandbox-topology/topology-definition#hosts).

You can specify additional Ansible host groups in [Topology definition](/sandboxes/sandbox-topology/topology-definition#groups) and then use them in a `playbook.yml` file of the [User Ansible](#user-ansible).

### Ansible Special Variables

On top of [Ansible special variables](https://docs.ansible.com/ansible/latest/reference_appendices/special_variables.html), the KYPO sandbox-service defines more special variables.

* **kypo_global_openstack_stack_id**: the ID of sandbox representation in OpenStack cloud.
* **kypo_global_pool_id**: the ID of the pool for which the sandbox was created.
* **kypo_global_sandbox_allocation_unit_id**: the ID of the sandbox allocation unit. Once the sandbox is fully provisioned, it is the same ID as the sandbox ID.
* **kypo_global_sandbox_ip**: the sandbox IPv4 address.
* **kypo_global_sandbox_name**: the sandbox name, which is the compound of [stack_name_prefix](/installation/kypo-platform-configuration#sandbox-service), pool ID and sandbox allocation unit ID.
* **kypo_global_head_ip**: the KYPO head server IP address.

### Ansible Inventory

For each sandbox, the KYPO sandbox-service generates an `inventory.yml` file. It adds some networking data to it, which you might find useful in your [User Ansible](#user-ansible).

Example of inventory file for [small sandbox](https://gitlab.ics.muni.cz/kypo-crp/prototypes-and-examples/sandbox-definitions/small-sandbox).

```yaml
all:
  children:
    hosts:
      hosts:
        home:
          ansible_host: 172.16.2.230
          ansible_user: debian
        server:
          ansible_host: 172.16.2.13
          ansible_user: debian
    management:
      hosts:
        br:
          ansible_host: 172.16.0.216
          ansible_user: debian
          interfaces:
          - def_gw_ip: 203.203.203.206
            mac: fa:16:3e:bb:d5:0a
            routes: []
          - def_gw_ip: null
            mac: fa:16:3e:6a:dd:57
            routes:
            - gw: 100.100.100.3
              mask: 255.255.255.0
              net: 10.10.20.0
          - def_gw_ip: null
            mac: fa:16:3e:5c:3c:41
            routes:
            - gw: 200.100.100.3
              mask: 255.255.255.0
              net: 10.10.30.0
          ip_forward: true
        man:
          ansible_host: 201.201.2.133
          ansible_user: debian
          interfaces:
          - def_gw_ip: null
            mac: fa:16:3e:ee:1d:33
            routes:
            - gw: 203.203.203.111
              mask: 255.255.255.248
              net: 100.100.100.0
            - gw: 203.203.203.111
              mask: 255.255.255.0
              net: 10.10.20.0
            - gw: 203.203.203.111
              mask: 255.255.255.248
              net: 200.100.100.0
            - gw: 203.203.203.111
              mask: 255.255.255.0
              net: 10.10.30.0
          ip_forward: true
          user_private_key_path: /root/user_key
          user_public_key_path: /root/user_key.pub
        uan:
          ansible_host: 172.16.2.3
          ansible_user: debian
          interfaces:
          - def_gw_ip: 202.202.202.194
            mac: fa:16:3e:b1:86:44
            routes: []
          ip_forward: false
    routers:
      hosts:
        home-router:
          ansible_host: 172.16.1.228
          ansible_user: debian
          interfaces:
          - def_gw_ip: 200.100.100.4
            mac: fa:16:3e:0b:17:ed
            routes: []
          ip_forward: true
        server-router:
          ansible_host: 172.16.0.21
          ansible_user: debian
          interfaces:
          - def_gw_ip: 100.100.100.4
            mac: fa:16:3e:1b:38:6a
            routes: []
          ip_forward: true
    user-accessible:
      hosts:
        home: null
        home-router: null
  vars:
    kypo_global_openstack_stack_id: b76e13b4-ae59-4aaa-bc42-97b78780bdcc
    kypo_global_pool_id: 1
    kypo_global_sandbox_allocation_unit_id: 42
    kypo_global_sandbox_ip: 192.168.64.238
    kypo_global_sandbox_name: db-attack-42
    kypo_global_head_ip: 172.19.0.22
```
