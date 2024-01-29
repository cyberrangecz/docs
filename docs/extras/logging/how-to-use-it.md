## Enable command logging (Currently supported for Debian-based images)
Command logging was originally enabled on host VMs by using three Ansible roles. These roles enable Bash command logging, Metasploit framework command logging, and forwarding of logs from `host` VM to the `MAN`. These three roles have been united under a [KYPO Sandbox Logging role](https://gitlab.ics.muni.cz/muni-kypo/ansible-roles/sandbox-logging), which must be added to the sandbox definition's playbook to enable the functionality (More about sandbox definition creation: [Create Sandbox Definition](../../user-guide-basic/sandbox-agenda/sandbox-definition.md#create-sandbox-definition)).

## Accessing logged data
The training organizer can access all logged data (training events or commands) by exporting the training instance in the [Training Instance Overview](../../user-guide-basic/training-agenda/training-instance.md#training-instance-overview). All data can be found in the exported archive in the corresponding files stored in the JSON format.

![Archive](../../img/extras/logging/accessed-logged-data-structure.png)


## Local deployment with vagrant

If you are using the local vagrant deployment configuration from the [kypo-crp](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment) project and want to access logged data via the [Training Instance Overview](../../user-guide-basic/training-agenda/training-instance.md#training-instance-overview), you need to additionally set up the forwarding from `MAN` to your local machine. To manually set up this forwarding, follow these steps.


**1. Create a new port forwarding rule in VirtualBox Manager (configured on Ubuntu):**

Open the VirtualBox Manager, and in the `Advanced Network settings` of your KYPO VM session, click on the **Port Forwarding** button:
![VirtualBox settings](../../img/extras/logging/port-forwarding-rule.png)

The `Port Forwarding Rules` create a new rule for log forwarding with `Guest IP` of `172.19.0.22`, `Guest Port` of `515`, and with any `Host port`, e.g., `8015`. For example, the `Log Forwarding` rule:

![PortForwardingRules](../../img/extras/logging/port-forwarding-rule2.png)

**2. Set the KYPO Head IP for sandbox service:**

Open the [main.yml](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment/-/blob/master/provisioning/roles/kypo-crp-head/defaults/main.yml) file (located in the `/kypo-crp-deployment/provisioning/roles/kypo-crp-head/defaults/main.yml`) and set the `kypo_head_ip` to the IP address of your local machine.

!!! note
    If you don't change the `kypo_head_ip` variable, all logs will be stored on the **MAN** in the `/data/idm-logs/man.log` file.

!!! note
    You can check if your data are getting into the ELK infrastructure by using the following command inside the `elasticsearch` docker container to list all data stored in the Elasticsearch:
    ```
    curl -XGET "http://localhost:9200/kypo*/_search?pretty=true"
    ```

**3. Start the KYPO platform:**

After updating the file with default variables, you can start the KYPO platform by following the [manual](https://gitlab.ics.muni.cz/muni-kypo-crp/devops/kypo-crp-deployment#run-vagrant-vm). If the KYPO platform is already running, you can apply the changes by running the following command in the `/kypo-crp-deployment` directory: 
```
EXTRA_VARS=./local-demo-extra-vars.yml,./local-demo-secrets.yml vagrant up --provision
```

**4. Update syslog-ng configuration in the MAN:**

After you have built your sandbox, you need to change the forwarding of the syslog-ng in the MAN. Access the MAN via ssh (How to access MAN: [Sandbox SSH Access](../../user-guide-advanced/sandboxes/sandbox-access.md)). When you are in the MAN open the syslog-ng log forwarding configuration:
```
sudo vim /etc/syslog-ng/conf.d/forward-rfc5424-messages.conf
```

Here in the `destination d_kypo_head` section change the `port(515)` to the Host port you set in the VirtualBox Manager in the first step and save your changes. Following the example from the first step your configuration should look like this (with an exception in IP address, which should be the one you set in the second step):
```
# EVENTS Log Source
source s_host {
    network(
       ip(0.0.0.0)
       port(514)
       transport(tcp)
       flags(syslog-protocol)
    );
};

destination d_kypo_head {
    network(
        "147.251.69.18"
        port(8015)
        transport(tcp)
        ip-protocol(4)
        flags(syslog-protocol)
    );
};

# EVENTS Log Pairing
log {source(s_host); destination(d_kypo_head);};
```

**5. Restart the syslog-ng service on MAN:**

As the last step you need to the restart syslog-ng service on the MAN by using the following command:

```
sudo systemctl restart syslog-ng.service
```

Wait a few seconds until the syslog-ng restarts.

## View Data In Kibana

1. Export data from KYPO Platform. On the [Training Instance Overview page](../../user-guide-basic/training-agenda/training-instance.md#training-instance-overview), click the :material-dots-vertical:{: .grey .icon} button and then click the **Get Data** button to export the training instance results in the ZIP archive. 

2. Extract the ZIP file to the arbitrary folder. 

3. Download the [elk-portal-commands-events project](https://gitlab.fi.muni.cz/cybersec/elk-la/elk-portal-commands-events) from GitLab and follow the instructions in the [README](https://gitlab.fi.muni.cz/cybersec/elk-la/elk-portal-commands-events/-/blob/master/README.md) file of the project.
