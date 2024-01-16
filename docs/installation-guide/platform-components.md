KYPO Platform has been designed as a web application that uses the microservice architecture style. The concept of microservices consists in the separation of individual logical units into separate parts, which provide certain specific functionality. The architecture of the KYPO platform is displayed in the picture below.


![microservices](../img/installation-guide/kypo-microservices.png)

## KYPO Head
KYPO Head is a host on which all essential services are running.

### User And Group Service
Provides functionality to manage users, groups, roles in the KYPO platform and allows registration of other microservices with specific roles. An administrator manages those entities. Administrators can manipulate users (add/remove them to/from created groups) and groups (create or remove them, assign/unassign roles to/from groups) and register new external microservices.

### Training Service
It is used to create, manage, and perform **linear** cybersecurity trainings in the form of multi-level trainings featuring the sandboxes. Sandboxes are created by [Sandbox Service](#sandbox-service) via cloud service, and they are accessible using SPICE console or using SSH. Besides that, all events during the training (training started, solution taken, entered commands in the command line of VMs, etc.) are recorded and stored in the Elasticsearch database. These data are then used to visualize the progress of one particular trainee or all trainees.

### Answers Storage
Stores unique answers for each sandbox under the specific identifier. Answers are generated during the allocation of the sandbox, and then they are requested by [Training Service](#training-service) when evaluating a submitted answer of the trainee for a particular level. 

### Training Feedback Service
Provides data necessary to visualize the feedback in the form of three types of graphs: summary, reference, trainee. The creation of the graphs is conditioned by semantical and syntax analysis of the commands executed during the training. Commands are then compared against the reference solution, and the data for respective graphs are generated. A detailed description of the graphs can be found in the section [Visualizations for Linear Training](../user-guide-basic/training-agenda/visualizations/visualizations-for-linear.md).


### Adaptive Training Service
It is used to create, manage, and perform **adaptive** cybersecurity trainings in the form of multi-phases trainings featuring the sandboxe. Sandboxes are used in a similar way as in Training Service. The assignments of phases are adapted to the trainees' skills and experiences. All events recorded and stored in the Elasticsearch database are used to compute the most suitable assignment for the trainee. The computation is done by the [Smart Assistant](#smart-assistant-service). 

### Smart Assistant Service
Based on the input from the Adaptive Training Service and obtained statistics about previous events from Elasticsearch Service, it computes the most suitable assignment for the trainee.

### Elasticsearch Service
This service aims to communicate with and obtain queried data (events and commands from the trainings)  from Elasticsearch. Microservice provides several endpoints to get different data portions, e.g., events per one training or multiple trainings.

### Sandbox Service
Provides functionality to manage the lifecycle of sandboxes in the KYPO platform. It includes managing sandbox definitions, creating sandboxes, their removal, configuration, networking inside of sandboxes, or user configuration of machines. Description of sandbox topology can be found in section [Sandboxes](../user-guide-advanced/sandboxes/topology-definition.md).

### OIDC Provider
Service is realized by OpenID Connect, which is used to authenticate the users logged into the KYPO Platform and obtain basic profile information about the end-user in an interoperable and REST-like manner. It provides a secure authentication mechanism for microservices and the protection of their APIs.

### Mitre Technique Service
Provides a visualization of [MITRE ATT&CK matrix](https://attack.mitre.org/), extended by additional information about which training definitions focus on specific tactics. Two versions of this matrix can be requested. The first version has all training definitions, and the second version has definitions that a particular player has played.

### Angular Frontend
User-friendly graphical user interface implemented using the Angular framework. Provides access to individual microservices and their selected functionalities via a web browser. 

## Third-Party Components

### Cloud Service
External service serves as a provider of compute, storage, and networking resources. Currently, the KYPO platform supports only the OpenStack cloud service.

!!! note
    The part of the KYPO which is responsible for catching, processing, and storing events from training microservice or commands from VMs of sandboxes is not displayed in the picture. Architecture of this part of the platform is described in section [Logging](../extras/logging/architecture.md).
