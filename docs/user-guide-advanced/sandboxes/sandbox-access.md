## Sandbox

A Topology Instance of a Sandbox is created in the cloud platform and connected to the [Base Infrastructure](../../installation-guide/installation-guide-overview.md), which mainly consists of 2 servers and a network.

* **Kubernetes Cluster node**: The server where the CyberRangeCZ Platform is installed.
* **Proxy Jump**: The server is used only for SSH access to all sandboxes.
* **Base Network**: The network where both servers and all sandboxes are connected through MAN ([more about management nodes](topology-instance.md#topology-instance-management)).

![Topology diagram](/img/user-guide-advanced/sandboxes/topology-instance.svg){: .center style="max-height: 800px;"}

!!! note
    For clarity reasons, there are missing links from **man-network** to the left **Router** and left **Host**.

## Sandbox Access

Sandbox access is divided into two major categories:

* [Terminal Remote Access](#terminal-remote-access):  Access to the remote sandbox node from the local command-line interface. It requires additional configuration. We differentiate two types based on privileges:
     * [Management access](#management-access) is available for those who manage sandboxes or CyberRangeCZ Platform (role `instructor`).
     * [User access](#user-access) is provided for everyone else (role `trainee`).
* [Web-based Access](#web-based-access): Access to the remote sandbox node through the CyberRangeCZ Platform portal in the web browser is available for everyone. It is simpler because it doesn't require any additional configuration. We support [Apache Guacamole](#apache-guacamole).


### Terminal Remote Access

!!! note
    Windows users must install `Git Bash` or `WSL`. On Windows, all actions in Management access and User access to connect to the sandboxes have to be performed using the `Git Bash` or `WSL` console. Please note that creating the `.ssh` folder is not required. The' Extract action' will be created automatically using the `unzip` command.


#### Management Access

Access to the sandbox nodes is through the **Proxy Jump**, and a **MAN** node as jump hosts and a **man-network**.

1. Download the SSH access zip file from [Pool Overview](../../user-guide-basic/sandbox-agenda/pool.md#pool-overview) page.

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

3. Connect to any virtual machine specified in the SSH configuration file except **Proxy Jump**.

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

#### User Access
Access to the sandbox nodes is through the **Proxy Jump**, and a **MAN** node, as jump hosts and an `accessible_by_user` networks.

!!! warning "Sandbox definition set up"
    You will not be able to use this approach if you did not set up the sandbox definition correctly!

    * Set user access to networks in the sandbox definition file `topology.yml`, e.g., set an attribute `accessible_by_user` of the network to value `True` or leave it undefined as it is a default value. See [Topology Definition](topology-definition.md#networks).

    * Set user access to hosts connected to user-accessible networks, e.g., apply Ansible role [user-access](https://github.com/cyberrangecz/ansible-role-user-access) to specified hosts in the file `provisioning/playbook.yml` of the sandbox definition.

    !!! warning
        The SSH config file will be generated with the host's directive `User` set to `user-access`, therefore setting variable `user_access_username` to value `user-access` modify the SSH config file later.

1. Download the SSH access zip file from [Training Level](../../user-guide-basic/training-agenda/training-run/linear-training-run.md#3-training-level) of the Linear Training Run page with topology visualization (in case of Adaptive Training Run, download it from the [Training Phase](../../user-guide-basic/training-agenda/training-run/adaptive-training-run.md#3-training-phase)).

2. Extract the `ssh-access.zip` file to the `~/.ssh/` directory.

    ```shell
    $ unzip ssh-access.zip -d ~/.ssh/
    ```

    Extracted files:

    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-config`: the SSH configuration file.
    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-key`: the sandbox user SSH private key.
    * `~/.ssh/pool-id-ID-sandbox-id-ID-user-key.pub`: the sandbox user SSH public key.

3. Connect to any virtual machine specified in the SSH configuration file except **Proxy Jump**, **MAN**.

   * Connect directly to any virtual machine using SSH protocol, even a Windows machine, e.g.:

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config <vm_name>
       ```

   * Connect to any virtual machine using software that supports communication over SOCKS5 proxy.
     First, create a local proxy on a port 12345:

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config -N -D 12345 man
       ```

     Then connect to a virtual machine specified in the SSH configuration file over `socks5://localhost:12345` proxy.

   * If the communication software does not support SOCKS5 proxy like Windows RDP client,
     use local port forwarding to bind the virtual machine's port to your localhost.
     For example, bind the virtual machine's RDP server port 3389 to your local port 12345.
     Virtual machine IP is specified in the SSH configuration file.

       ```shell
       $ ssh -F ~/.ssh/pool-id-ID-sandbox-id-ID-user-config -N -L 12345:<vm_ip>:3389 man
       ```

     Then use the RDP client and connect to a virtual machine using the `localhost:12345` address.

### Web-based Access
Simple access to the sandbox node from within the web browser is available through the CyberRangeCZ Platform portal from the sandbox topology. An instructor can display the topology on the [Pool Detail](../../user-guide-basic/sandbox-agenda/pool.md#pool-detail) page, and for trainees, the topology is always displayed during a training run in [training levels](../../user-guide-basic/training-agenda/training-run/linear-training-run.md#3-training-level). Right-click on the selected network node (host or router) in the network topology will open the menu with the following options (see [VM manipulation](../../user-guide-basic/training-agenda/training-run/linear-training-run.md#vm-manipulation):

* **Open console**: Opens the command-line interface (CLI) in [Apache Guacamole](#apache-guacamole) application using the SSH protocol. This option is available only for routers and hosts with Linux-based operating systems.
* **Open GUI**: Opens graphical user interface (GUI) in [Apache Guacamole](#apache-guacamole) application using the VNC or RDP protocol. This option can be available for all routers and hosts but depends on whether they are properly configured.

!!! warning "Credentials"
    A user must know the login credentials to access the sandbox node in all cases. Upon entering invalid credentials, the [Apache Guacamole](#apache-guacamole) connection will be closed immediately.

#### Apache Guacamole
An HTML5 web application supports graphical access to remote hosts directly in the browser. It is a clientless remote desktop gateway that supports standard protocols like VNC, RDP, and SSH. In the CyberRangeCZ Platform, all the mentioned protocols can be used, but the following conditions must be satisfied:

1. **SSH** (only Linux-based system): The target host must have allowed password authentication. This can be done by setting up the following parameter in `/etc/ssh/sshd_config`:
      ```
      PasswordAuthentication yes
      ```
2. **VNC** (only Linux-based system): Requires running VNC server with possible login option. Configuration of the VNC server may vary based on the OS type and its version.
3. **RDP** (Windows): Requires enabled *Remote Desktop*.

!!! warning "VNC & RDP"
    Besides the proper configuration, the image of the machines must have set the custom property `owner_specified.openstack.gui_acess` to `true`. Otherwise, the option `Open GUI` in the topology won't be available.


