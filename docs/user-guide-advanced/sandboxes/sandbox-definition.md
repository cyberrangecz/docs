The Sandbox Definition is a directory structure stored as a Git repository managed by CyberRangeCZ Platform instructors to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── topology.yml
├── variables.yml
└── provisioning/
    └── playbook.yml
└── preconfig/
```

* **topology.yml**: a [Topology Definition](topology-definition.md) of a topology that will be deployed in the cloud. Once deployed it is called [Topology Instance](topology-instance.md).

* **variables.yml (optional)**: a configuration file containing all necessary and optional information for the generation of [APG Variables](apg-variables.md) that can be used to create variant answers for the sandboxes in the pool. It's necessary for APG trainings.

* **provisioning**: a directory structure of a [Sandbox Provisioning](sandbox-provisioning.md) which is intended for [Topology Instance](topology-instance.md) customization. Once provisioned it is called a Sandbox.
