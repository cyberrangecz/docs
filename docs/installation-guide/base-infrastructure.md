## Prerequisites

* Install APT packages

    ```shell
    $ sudo apt install python-pip
    ```
    
* Install Python packages

    ```shell
    $ sudo pip install "openstacksdk==0.43.0" "python-openstackclient==5.2.1" "python-heatclient==1.18.0"
    ```
    
* [Obtain Application Credentials](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo2-openstack-deploy/-/wikis/how-to/Obtain-Application-Credentials)
    and source `app-cred-<name>-openrc.sh` file before the first use of a new terminal session.

    ```shell
    $ source /path/to/app-cred-<name>-openrc.sh
    ```

## Configuration

There are 3 configuration files. Each for a different OpenStack project.

| OpenStack project     | Configuration file                       |
| -----------------     | ------------------                       |
| kypo-platform-devel   | [devel-params.yml](configuration-files/devel-params.yml)     |
| kypo-platform-staging | [staging-params.yml](configuration-files/staging-params.yml) |
| kypo-platform-testing | [testing-params.yml](configuration-files/testing-params.yml) |

Before you get to the deployment choose one of the configuration files and follow the next steps.

1. Check that both floating IP IDs exists in the OpenStack project (i.e. `kypo_base_head_floating_ip_id` and `kypo_base_proxy_floating_ip_id`).

    List Floating IP addresses in the OpenStack project.

    ```shell
    $ openstack floating ip list
    ```
    
    For each missing floating IP, create a new one and update IDs in the configuration file.
    
    Use the following command with parameter `kypo_base_external_public_network_name` or `kypo_base_external_private_network_name` respectively from the configuration file. Both of them are OpenStack external networks, where the first one can be used to allocate a public IP address and the second one to allocate a private IP address of your company. The choice depends on your needs but, typically only servers on kypo-platform-production and kypo-platform-devel OpenStack projects should have public IP addresses.
    
    ```shell
    $ openstack floating ip create <kypo_base_external_<public/private>_network_name>
    ```
    
2. Set both KeyPair names to OpenStack SSH KeyPair that you own private part of (i.e. `kypo_base_head_keypair_name` and `kypo_base_proxy_keypair_name`).
    It can be the same KeyPair for both servers KYPO-head and KYPO-proxy.

    List KeyPairs in the OpenStack project.

    ```shell
    $ openstack keypair list
    ```
    
    If you do not own the private part of any of the KeyPairs, add the public part of any of your SSH keys to OpenStack KeyPairs.
    
    ```shell
    $ openstack keypair create --public-key </path/to/id_rsa.pub> <kypo_base_<head/proxy>_keypair_name>
    ```

## Deployment

There are 4 files of HEAT templates. Each of them is used to create a different part of the base infrastructure. 

* [kypo-base-networking.yml](heat-templates/kypo-base-networking.yml): Creates a base network where all sandboxes, KYPO-head, and KYPO-proxy will be connected to.
    This template is designed for KYPO-head and KYPO-proxy to have public IP addresses.
* [kypo-base-networking-private.yml](heat-templates/kypo-base-networking-private.yml): Almost the same as the previous one but
    this template is designed for KYPO-head and KYPO-proxy to have private IP addresses.    
    **NOTE**: Do not use both networking templates.
* [kypo-head.yml](heat-templates/kypo-head.yml): Creates the KYPO-head server where the KYPO platform will be installed.
* [kypo-proxy-jump.yml](heat-templates/kypo-proxy-jump.yml): Creates the KYPO-proxy server which is used for users to access sandboxes.

### Create

1. Create KYPO-base networking, KYPO-head, and KYPO-proxy. First, choose the right networking template and the OpenStack project configuration. Then run the following commands.

    ```bash
    $ openstack stack create --wait -e <project>-params.yml -t <kypo-base-networking<-private>>.yml kypo-base-networking-stack
    $ openstack stack create --wait -e <project>-params.yml -t kypo-head.yml kypo-head-stack
    $ openstack stack create --wait -e <project>-params.yml -t kypo-proxy-jump.yml kypo-proxy-jump-stack 
    ```
    
2. All communication to the OpenStack project is prohibited by default.
    Set OpenStack [Firewall](#firewall) rules to enable communication.

3. Test SSH connection.

    Obtain `default_user` of the images used for KYPO-head and KYPO-proxy server
    (i.e. `kypo_base_head_image` and `kypo_base_proxy_image`).

    ```shell
    $ openstack image show <kypo_base_<head/proxy>_image> -f json -c properties
    ```
    
    Using floating IP address and KeyPair from [Configuration](#configuration)
    step with previously obtained `default_user` test that you can access both servers.
    
    ```shell
    $ ssh -i </path/to/id_rsa> <default_user>@<kypo_base_<head/proxy>_floating_ip> echo ok
    ```

### Delete

1. Before the base infrastructure deletion, you need to delete all stacks connected to it.

    List all existing stacks.

    ```shell
    $ openstack stack list
    ```

    Each KYPO platform instance is prefixing stack names with its identifier.
    Execute the following command for every KYPO platform instance that was using this base infrastructure.
    Replace the `<stack-name-prefix>` placeholder for example for `kypo-devel-`.
    
    ```shell
    $ openstack stack list | grep " <stack-name-prefix>" | awk '{print $2}' | xargs openstack stack delete --wait -y 
    ```
    
    Check that there is nothing connected to the base infrastructure. Everything is ok if there is no output.
    
    ```shell
    $ openstack port list | grep "subnet_id='$(openstack subnet list | grep kypo-base-subnet | awk '{print $2}')'"
    ```
    
2. Destroy the whole base infrastructure.
    **NOTE**: Delete the base networking last.
    
    ```bash
    $ openstack stack delete --wait -y kypo-head-stack
    $ openstack stack delete --wait -y kypo-proxy-jump-stack
    $ openstack stack delete --wait -y kypo-base-networking-stack
    ```

## Firewall

The firewall rules within OpenStack are grouped in Security Groups.
Currently, we are using only the default Security Group called `default`.
By default, all egress communication is allowed, but ingress communication is allowed only within the same Security Group.

List all Security Group rules.

```shell
$ openstack security group rule list <security-group>
```

KYPO platform currently requires ingress access only for ports 22 (SSH)
and 443 (HTTPS), and optionally ingress access of ICMP protocol.

```shell
$ openstack security group rule create --remote-ip 147.251.0.0/16 --protocol icmp --ingress --ethertype IPv4 <security-group>
$ openstack security group rule create --remote-ip 147.251.0.0/16 --dst-port 22 --protocol tcp --ingress --ethertype IPv4 <security-group>
$ openstack security group rule create --remote-ip 147.251.0.0/16 --dst-port 443 --protocol tcp --ingress --ethertype IPv4 <security-group>
```

For more information run help of the create or delete command.
