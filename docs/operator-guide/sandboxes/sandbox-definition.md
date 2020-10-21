The Sandbox Definition is a Gitlab repository managed by KYPO organizers to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── sandbox.yml
└── provisioning/
    └── playbook.yml
```

* **sandbox.yml**: a [Topology Definition](../sandbox-topology/topology-definition) of a topology that will be deployed in the cloud. Once it is deployed we call it [Topology Instance](../sandbox-topology/topology-instance).
* **provisioning**: a directory structure of a [User Ansible](../user-ansible) which is intended for [Topology Instance](../sandbox-topology/topology-instance) customization. Once it is provisioned we call it a Sandbox.
