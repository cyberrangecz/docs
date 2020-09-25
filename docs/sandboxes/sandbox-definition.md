The Sandbox Definition is a Gitlab repository managed by KYPO organizers to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── sandbox.yml
└── provisioning/
    └── playbook.yml
```

* **sandbox.yml** - A [Topology Definition](/sandboxes/sandbox-topology/topology-definition) of a topology that will be deployed in the cloud. Once it is deployed we call it [Topology Instance](/sandboxes/sandbox-topology/topology-instance).
* **provisioning** - A directory structure of a [User Ansible](/sandboxes/user-ansible) which is intended for [Topology Instance](/sandboxes/sandbox-topology/topology-instance) customization. Once it is provisioned we call it a Sandbox.
