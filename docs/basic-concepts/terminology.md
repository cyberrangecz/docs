Before you start with the KYPO CRP, you need to have a general understanding of the objects used in the context of the platform. This topic briefly introduces you to a few basic terms which help you get started with KYPO CRP faster.

## Emulated Virtual Environment
When creating and using an emulated virtual environment we use the following terminology:

* **[Sandbox](../../user-guide-advanced/sandboxes/sandboxes-overview/#sandbox):** It is an isolated testing environment with virtual networks that enable users to connect to the virtual machines (VMs) and communicate with the rest of the network, the host machine, and other VMs. At the VMs, the user can run programs, use network services, or monitor the network traffic. Everything without affecting the external infrastructure. Sandbox is created using cloud service.
* **[Sandbox Definition](../../user-guide-advanced/sandboxes/sandboxes-overview/#sandbox-definition):** Definition of the internal structure of the sandboxes (networks and hosts) and user customization of the hosts. It consists of two parts: [Topology Definition](../../user-guide-advanced/sandboxes/sandbox-topology/topology-definition) and [Sandbox Provisioning](../../user-guide-advanced/sandboxes/sandbox-provisioning).
* **[Pool](../../user-guide-advanced/sandboxes/sandboxes-overview/#pool):** A group of sandboxes created based on the same sandbox definition.

## Training
KYPO training is centred around the sandbox, where trainees solve tasks presented in KYPO GUI. KYPO training can also contain questionnaires to collect feedback from trainees or test to asses their knowledge. In the context of the training we use the following terminology:

* **[Training Definition](../../user-guide-advanced/trainings/trainings-overview#training-definition):** Defines the scenario of the training. It is composed of several levels. Each level can be of different types: Game level, Assessment level, Info level.
* **[Training Instance](../../user-guide-advanced/trainings/trainings-overview#training-instance):** Specify the time period in which the players can access training. Each training instance also must be assigned a pool of sandboxes.
* **[Training Run](../../user-guide-advanced/trainings/trainings-overview#training-run):** Single run of training of the particular player. Each run has an assigned sandbox from the pool.
