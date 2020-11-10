KYPO Platform has been designed as a web application that uses the microservice architecture style. The concept of microservices consists in the separation of individual logical units into separate parts, which provide certain specific functionality. The architecture of the KYPO platform is displayed in the picture below.


![microservices](../img/user-guide-advanced/platform-components/kypo-microservices.png)

## KYPO Head
KYPO Head is a host on which all essential services are running.

### User And Group Service
Provides functionality to manage users, groups, roles in the KYPO platform and allows registration of other microservices with other specific roles. Those entities are managed by an administrator. Administrator can manipulate with users (add/remove them to/from created groups) and groups (create or remove them, assign/unassign roles to/from groups), and can register new external microservices.

### Training Service
It is used to create, manage, and perform cybersecurity trainings in form of multi-level games featuring the sandboxes. Sandboxes are created by [Sandbox Service](#sandbox-service) via cloud service and they are accessible using SPICE console or using SSH. Besides that, all events during the training (game started, solution taken, entered commands in the command line of VMs, etc.) are recorded and stored in the Elasticsearch database. These data are then used to visualize the progress of one particular trainee or all trainees.

### Elasticsearch Service
The purpose of this service is to communicate with and obtain queried data (events and commands from the trainings)  from Elasticsearch. Microservice provides several endpoints to obtain different portions of data, e.g. events per one game or events per multiple games.

### Sandbox Service
Provides functionality to manage the lifecycle of sandboxes in the KYPO platform. It includes managing sandbox definitions, creating sandboxes, their removal, configuration, networking inside of sandboxes, or user configuration of machines. Description of sandbox topology can be found in section [Sandboxes](../../user-guide-advanced/sandboxes/sandbox-topology/topology-definition).

### OIDC Provider
Service realized by OpenID Connect, which is used to authenticate the users logged into the KYPO Platform, as well as to obtain basic profile information about the end-user in an interoperable and REST-like manner. It provides a secure authentication mechanism for microservices and protection of their APIs.

### Angular Frontend
User-friendly graphical user interface implemented using the Angular framework. Provides access to individual microservices and their selected functionalities via a web browser. 

## Third-Party Components

### Cloud Service
External service serves as a provider of compute, storage, and networking resources. Currently, the KYPO platform supports only the OpenStack cloud service.

!!! note
    The part of the KYPO which is responsible for catching, processing, and storing events from training microservice or commands from VMs of sandboxes is not displayed in the picture. Architecture of this part of the platform is described in section [Logging](../extras/logging/architecture.md).
