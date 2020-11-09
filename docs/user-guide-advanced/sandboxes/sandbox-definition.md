The Sandbox Definition is a directory structure stored as a Git repository managed by KYPO instructors to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── sandbox.yml
└── provisioning/
    └── playbook.yml
```

* **sandbox.yml**: a [Topology Definition](../sandbox-topology/topology-definition) of a topology that will be deployed in the cloud. Once it is deployed we call it [Topology Instance](../sandbox-topology/topology-instance).
* **provisioning**: a directory structure of a [Sandbox Provisioning](../sandbox-provisioning) which is intended for [Topology Instance](../sandbox-topology/topology-instance) customization. Once it is provisioned we call it a Sandbox.
