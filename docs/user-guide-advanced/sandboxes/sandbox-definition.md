The Sandbox Definition is a directory structure stored as a Git repository managed by KYPO instructors to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── topology.yml
└── provisioning/
    └── playbook.yml
```

* **topology.yml**: a [Topology Definition](../topology-definition/) of a topology that will be deployed in the cloud. Once deployed it is called [Topology Instance](../topology-instance/).

    !!! note
        The name **sandbox.yml** is deprecated since version 21.06.

* **provisioning**: a directory structure of a [Sandbox Provisioning](../sandbox-provisioning/) which is intended for [Topology Instance](../topology-instance/) customization. Once provisioned it is called a Sandbox.
