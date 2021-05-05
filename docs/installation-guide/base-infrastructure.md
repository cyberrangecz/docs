# Base Infrastructure

This page contains the steps that are needed to prepare the KYPO base
infrastructure used by the KYPO Cyber Range Platform.

## Prerequisites

KYPO Cyber Range Platform is tested with Open Stack releases Stein and Train, but it is quite possible it will also work on newer releases.

At this moment, you should have installed [OpenStack](https://docs.openstack.org/install-guide/) with the following [OpenStack Services](https://www.openstack.org/software/project-navigator/openstack-components).

- Nova
- Neutron
- Keystone
- Placement
- Heat
- Horizon

For every instance of KYPO Cyber Range Platform you also need two floating addreses from Open Stack public pool to access the platform.

## Toolkit

The following instructions were tested on **Debian**-like OS, specifically Linux Mint 19, 20 and Ubuntu 20.

| Tool                  | Version |
| ----                  | ------  |
| Python                | 3.8     |
| Pipenv                | 2020+   |
| openssh-client        | 1.7     |
| jq                    | 1.6     |

1. Install APT packages

    ```shell
    sudo apt install python3-pip openssh-client jq
    ```

2. Install Pipenv

    ```shell
    sudo pip3 install pipenv
    ```

3. [Obtain Application Credentials](https://docs.openstack.org/keystone/ussuri/user/application_credentials.html) and source `app-cred-<name>-openrc.sh` file before the first use of a new terminal session. Application Credentials needs to be generated with the parameter **unrestricted**.

    ```shell
    source /path/to/app-cred-<name>-openrc.sh
    ```

4. Clone [KYPO CRP base repository](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-openstack-base)

    ```shell
    git clone https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-openstack-base.git
    cd kypo-crp-openstack-base
    ```

    Don't leave this directory!

5. Install the necessary dependencies via Pipenv

    ```shell    
    pipenv install
    pipenv shell
    ```
    Don't leave the Pipenv shell!

## Configuration

Before you get to the deployment, you must obtain several configuration values that might be specific to your OpenStack instance.

1. Get the name of the OpenStack external network that will allow you to allocate floating IP addresses from public IP address range.

    List all external networks.

    ```shell
    openstack network list --external --column Name
    ```

    Expected output.

    ```shell
    +--------------------------+
    | Name                     |
    +--------------------------+
    | <kypo_base_external_net> |
    +--------------------------+
    ```

2. Get the image names that will be used for the KYPO base servers.

    List all images.

    ```shell
    openstack image list --column Name
    ```

    Expected output.

    ```
    +-------------------+
    | Name              |
    +-------------------+
    | <kypo_base_image> |
    +-------------------+
    ```

    (This guide was tested on Ubuntu-based images).

3. Get the flavor names that will be used for the KYPO base servers.

    List all flavors.

    ```shell
    openstack flavor list --column Name
    ```

    Expected output.

    ```
    +--------------------+
    | Name               |
    +--------------------+
    | <kypo_base_flavor> |
    +--------------------+
    ```

    (This guide was tested with flavors of 4 VCPUs, 16384 RAM 80 GB Disk and 2 VCPUs, 4096 RAM, 80 GB Disk).

4. Edit the desired values for images (`<kypo_base_image>`) and flavors (`<kypo_base_flavor>`) in the `openstack-defaults.sh` file of the cloned repository. Source `openstack-defaults.sh` file.

    The default values are set as follows.

    ```shell
    export KYPO_HEAD_FLAVOR="standard.large"
    export KYPO_HEAD_IMAGE="ubuntu-focal-x86_64"
    export KYPO_PROXY_FLAVOR="standard.medium"
    export KYPO_PROXY_IMAGE="ubuntu-focal-x86_64"
    ```

    ```shell
    source openstack-defaults.sh
    ```

5. Delete all non-default Security Group Rules from the `default` Security Group (they serve as a firewall).

    List all groups.

    ```
    openstack security group rule list default
    ```

    Expected state.

    ```
    +-----------+-------------+-----------+-----------+------------+-----------------------+
    | ID        | IP Protocol | Ethertype | IP Range  | Port Range | Remote Security Group |
    +-----------+-------------+-----------+-----------+------------+-----------------------+
    | <rule_id> | None        | IPv4      | 0.0.0.0/0 |            | ...                   |
    | <rule_id> | None        | IPv4      | 0.0.0.0/0 |            | None                  |
    | <rule_id> | None        | IPv6      | ::/0      |            | None                  |
    | <rule_id> | None        | IPv6      | ::/0      |            | ...                   |
    +-----------+-------------+-----------+------------------------+-----------------------+
    ```

    Delete any unwanted rules by issuing the following command.

    ```
    openstack security group rule delete <rule_id>
    ```

## Deployment

1. Bootstrap Floating IPs and Keypair. The results will be saved into `kypo-base-params.yml` file.
Private key of the keypair will be saved into `<ostack-project>_kypo-base-key.key`

    ```shell
    ./bootstrap.sh <kypo_base_external_net>
    ```

2. Create the base infrastructure.

    ```shell
    ./create-base.sh
    ```

3. Security Groups information.

    The firewall rules within OpenStack are grouped into Security Groups. KYPO platform currently requires the following rules to be enabled. They are created automatically in the previous step.

    * 22 (SSH)
    * 443 (HTTPS)
    * 8443 (HTTPS)
    * ICMP protocol

    !!! note
        The provided group rules are very basic and they expose the deployed servers to the world (`0.0.0.0/0`). This may not be suitable for your use case.

4. Test the base infrastructure via Ansible (executed with the `host_key_checking = False` option).

    ```shell
    ./ansible-check-base.sh
    ```

    Expected output (`failed=0`).

    ```shell
    # ...
    PLAY RECAP *******************************************************************************************************
    kypo-base-head             : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    kypo-base-proxy            : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    ```

5. Provision the Proxy to enable user SSH access to sandboxes via tunneling

    ```shell
    ./ansible-user-access.sh
    ```

    Expected output (`failed=0`).

    ```shell
    PLAY RECAP *******************************************************************************************************
    kypo-base-proxy            : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
    ```

## Cleanup

1. Delete the base infrastructure.

    ```shell
    ./delete-base.sh
    ```

1. Delete Floating IPs and Keypair.

    !!! warning
        This step is extremely destructive. It will delete all the results of the bootstrap step, including the files generated on the local machine.

    ```shell
    ./bootstrap-delete.sh
    ```
