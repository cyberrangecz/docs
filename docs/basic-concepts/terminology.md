Before you start with the KYPO CRP, you need to have a general understanding of the terminology used in the context of the platform. This topic briefly introduces you to a few basic terms which help you get started with KYPO CRP faster.

## Emulated Virtual Environment
When creating and using an emulated virtual environment, we use the following terminology:

* **[Sandbox](../user-guide-advanced/sandboxes/sandboxes-overview.md#sandbox):** It is an isolated testing environment with virtual networks that enable users to connect to the virtual machines (VMs) and communicate with the rest of the network, the host machine, and other VMs. At the VMs, the user can run programs, use network services, or monitor the network traffic. Everything without affecting the external infrastructure. Currently, we differentiate two types of sandboxes:
    * **Cloud** - sandbox runs within the cloud and is remotely accessible.
    * **Local** - sandbox is created within the user computer using the [Vagrant](https://www.vagrantup.com/) along with [VirtualBox](https://www.virtualbox.org/) virtualization tool.
* **[Sandbox Definition](../user-guide-advanced/sandboxes/sandboxes-overview.md#sandbox-definition):** Definition of the internal structure of the sandboxes (networks and hosts) and user customization of the hosts. It consists of two parts: [Topology Definition](../user-guide-advanced/sandboxes/topology-definition.md) and [Sandbox Provisioning](../user-guide-advanced/sandboxes/sandbox-provisioning.md).
* **[Pool](../user-guide-advanced/sandboxes/sandboxes-overview.md#pool):** A group of **cloud** sandboxes created based on the same sandbox definition.

## Training
KYPO training is centered around the sandbox, where trainees solve tasks presented in KYPO GUI. KYPO training can also contain questionnaires to collect feedback from trainees or tests to assess their knowledge. In the context of the training, we use the following terminology:

* **[Training Definition](../user-guide-advanced/trainings/trainings-overview.md#training-definition):** Defines the scenario of the training. Based on their type, definitions can be composed either of levels or phases. Linear definitions can contain Training levels, Assessment levels, and Info levels. Adaptive definitions can be composed of Training phases, Questionnaire phases, and Info phases.
* **[Training Instance](../user-guide-advanced/trainings/trainings-overview.md#training-instance):** Specify the time period in which the players can access training. Each training instance also define one of the following environments:

    * **Cloud Environment (default)** - cloud sandboxes are used during the training. A pool of sandboxes must be assigned to the training instance.
    * **Local Environment** - local sandboxes are used during the training. A sandbox definition can be assigned to the training instance, so the trainees can take a look at topology.

* **[Training Run](../user-guide-advanced/trainings/trainings-overview.md#training-run):** Single run of training of the particular trainee. Each run has an assigned sandbox from the pool or use their own local sandbox.
