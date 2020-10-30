Before you start with the KYPO CRP, you need to have a general understanding of the objects used in the context of the platform. This topic briefly introduces you to a few basic terms which help you get started with KYPO CRP faster.

## Emulated Environment
When creating and using an emulated environment we use the following terminology:

* **Sandbox:** It is an isolated emulated testing environment that enables users to run programs or execute files without affecting the external infrastructure. Sandbox is created using cloud service.
* **Sandbox Definition:** Definition of the internal structure of the sandboxes (networks and hosts) and user customization of the hosts. It consists of two parts: Topology Definition and User Ansible.
* **Pool:** A group of sandboxes created based on the same sandbox definition.

For more detailed information check the section [Sandboxes](../operation-guide/sandboxes/sandboxes-overview).

### Training
The principle of ​​the KYPO CRP training is built on the previous idea of the emulated environment. Users can solve predefined cybersecurity tasks without interfering with the real infrastructure. In the context of the training we use the following terminology:

* **Training Definition:** Defines the scenario of the training. It is composed of several levels. Each level can be of different types: Game level, Assessment level, Info level.
* **Training Instance:** Specify the time period in which the players can access training. Each training instance also must be assigned a pool of sandboxes.
* **Training Run:** Single run of training of the particular player. Each run has an assigned sandbox from the pool.

For more detailed information about the trainings, check the section [Trainings](../operation-guide/trainings/trainings-overview).
