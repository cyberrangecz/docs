## Enable command logging (Currently supported for Debian-based images)
Command logging was originally enabled on host VMs by using three Ansible roles. These roles enable Bash command logging, Metasploit framework command logging, and forwarding of logs from `host` VM to the `MAN`. These three roles have been united under a [Sandbox Logging role](https://github.com/cyberrangecz/ansible-role-sandbox-logging), which must be added to the sandbox definition's playbook to enable the functionality (More about sandbox definition creation: [Create Sandbox Definition](../../user-guide-basic/sandbox-agenda/sandbox-definition.md#create-sandbox-definition)).

## Accessing logged data
The training organizer can access all logged data (training events or commands) by exporting the training instance in the [Training Instance Overview](../../user-guide-basic/training-agenda/training-instance.md#training-instance-overview). All data can be found in the exported archive in the corresponding files stored in the JSON format.

![Archive](/img/extras/logging/accessed-logged-data-structure.png)
