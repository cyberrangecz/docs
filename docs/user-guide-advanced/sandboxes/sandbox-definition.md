The Sandbox Definition is a directory structure stored as a Git repository managed by KYPO instructors to define a sandbox topology and provisioning of sandbox nodes.

The simplest directory structure of Sandbox Definition:

```
sandbox-definition/
├── topology.yml
├── variables.yml
└── provisioning/
    └── playbook.yml
└── preconfig/
```

* **topology.yml**: a [Topology Definition](../topology-definition/) of a topology that will be deployed in the cloud. Once deployed it is called [Topology Instance](../topology-instance/).

    !!! note
        The name **sandbox.yml** is deprecated since version 21.06.

* **variables.yml (optional)**: a configuration file containing all necessary and optional information for the generation of [APG Variables](../apg-variables/) that can be used to create variant answers for the sandboxes in the pool. It's necessary for APG trainings. 

* **provisioning**: a directory structure of a [Sandbox Provisioning](../sandbox-provisioning/) which is intended for [Topology Instance](../topology-instance/) customization. Once provisioned it is called a Sandbox.

* **preconfig (local sandbox definition only)**: contains files for the basic configuration of the created devices, like network configuration. These files should not be edited. For more information visit [wiki page](https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator/-/wikis/3.0/Generating-a-Sandbox#advanced-functionality) of CSC.
