## Sandbox

A Topology Instance of a Sandbox is created in the cloud platform and connected to the [KYPO Base Infrastructure](../../../installation-guide/base-infrastructure/), which mainly consists of 2 servers and a network.

* **KYPO Head**: The server where the KYPO platform is installed.
* **KYPO Proxy**: The server used only for SSH access to all sandboxes.
* **KYPO Base Network**: The network where both servers and all sandboxes are connected through MAN ([more about management nodes](../topology-instance/#topology-instance-management)).

![topology-instance-blank](../../img/user-guide-advanced/sandboxes/topology-instance-blank.png)

## Sandbox Access

Sandbox access is divided into two types based on privileges.[Management access](#management-access) is available for those who manage sandboxes or KYPO Cyber Range Platform (role `instructor`). [User access](#user-access) is provided for everyone else (role `trainee`).

!!! note
    Windows users are required to install WSL or Git Bash.

### Management Access

Access to the sandbox nodes is through the **KYPO Proxy**, and a **MAN** node as jump hosts and a **mng-network**.

1. Download the SSH access zip file from [Pool Overview](../../../user-guide-basic/sandbox-agenda/pool/#pool-overview) page.

2. Extract the `ssh-access.zip` file to the `.ssh/` folder in your home directory.

    ```shell
    $ unzip ssh-access.zip -d ~/.ssh/
    ```

    Extracted files:

    * `~/.ssh/pool-id-ID-sandbox-id-ID-management-config`: the SSH configuration file.
    * `~/.ssh/pool-id-ID-management-key`: the pool management SSH private key.
    * `~/.ssh/pool-id-ID-management-key.pub`: the pool management SSH public key.

    !!! note
        The configuration file is generated for every sandbox of the pool.

3. Connect to any virtual machine specified in the SSH configuration file except **KYPO Proxy**.

    * Connect directly to any virtual machine using SSH protocol, even a Windows machine, e.g.:

        ```shell
        $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-management-config man
        ```

    * Connect to any virtual machine using software that supports communication over SOCKS5 proxy.
        First, create a local proxy on a port 12345:

        ```shell
        $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-management-config -N -D 12345 man
        ```

        Then connect to a virtual machine specified in the SSH configuration file over `socks5://localhost:12345` proxy.

    * If the communication software does not support SOCKS5 proxy like Windows RDP client,
      use local port forwarding to bind the virtual machine's port to your localhost.
      For example, bind the virtual machine's RDP server port 3389 to your local port 12345.
      Virtual machine IP is specified in the SSH configuration file.

        ```shell
        $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-management-config -N -L 12345:<vm_ip>:3389 man
        ```

        Then use the RDP client and connect to a virtual machine using the `localhost:12345` address.

### User Access

Access to the sandbox nodes is through the **KYPO proxy**, a **MAN** node, and a **UAN** node as jump hosts and an `accessible_by_user` networks.

!!! warning "Sandbox definition set up"
    You will not be able to use this approach if you did not set up the sandbox definition correctly!

    * Set user access to networks in the sandbox definition file `topology.yml`, e.g., set an attribute `accessible_by_user` of the network to value `True` or leave it undefined as it is a default value. See [Topology Definition](../topology-definition/#networks).

    * Set user access to hosts connected to user-accessible networks, e.g., apply Ansible role [kypo-user-access](https://gitlab.ics.muni.cz/CSIRT-MU-public/ansible-roles/kypo-user-access/-/tree/master/) to specified hosts in the file `provisioning/playbook.yml` of the sandbox definition.

    !!! warning
        The SSH config file will be generated with the host's directive `User` set to `user-access`, therefore setting variable `kypo_user_access_username` to value `user-access` modify the SSH config file later.

1. Download the SSH access zip file from [Game Level](../../../user-guide-basic/training-agenda/training-run/#3-game-level) of the Training Run page with topology visualization.

2. Extract the `ssh-access.zip` file to the `~/.ssh/` directory.

    ```shell
    $ unzip ssh-access.zip -d ~/.ssh/
    ```

    Extracted files:

    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-config`: the SSH configuration file.
    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-key`: the sandbox user SSH private key.
    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-key.pub`: the sandbox user SSH public key.

3. Connect to any virtual machine specified in the SSH configuration file except **KYPO Proxy**, **MAN** or **UAN**.

   * Connect directly to any virtual machine using SSH protocol, even a Windows machine, e.g.:

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config <vm_name>
       ```

   * Connect to any virtual machine using software that supports communication over SOCKS5 proxy.
     First, create a local proxy on a port 12345:

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config -N -D 12345 uan
       ```

     Then connect to a virtual machine specified in the SSH configuration file over `socks5://localhost:12345` proxy.

   * If the communication software does not support SOCKS5 proxy like Windows RDP client,
     use local port forwarding to bind the virtual machine's port to your localhost.
     For example, bind the virtual machine's RDP server port 3389 to your local port 12345.
     Virtual machine IP is specified in the SSH configuration file.

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config -N -L 12345:<vm_ip>:3389 uan
       ```

     Then use the RDP client and connect to a virtual machine using the `localhost:12345` address.
