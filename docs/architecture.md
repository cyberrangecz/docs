KYPO Platform has been designed as a web application that uses the microservice architecture style. The concept of microservices consists in the separation of individual logical units into separate parts, which provide certain specific functionality. The architecture of the KYPO platform is displayed in the picture below.


![Architecture](img/kypo-architecture.png)

Among the main components of the KYPO platform belongs: 

* **User And Group Service**: Provides functionality to manage users, groups, roles in the KYPO platform and allows registration of other microservices with other specific roles. Those entities are managed by an administrator. Admin is able to manipulate with users (add/remove them to/from created groups) and groups (create or remove them, assign/unassign roles to/from groups), and can register new external microservices.
* **Training Service**: It is used to create, manage, and perform cybersecurity trainings in form of multi-levels games of type Capture The Flag. These games use sandboxes created by *Sandbox Service* via cloud service to give trainees their own virtual environment. Besides that, all events during the game (game started, solution taken, entered commands in the command line of machines, etc.) are recorded and stored in the Elasticsearch database. These data are then used to visualize the progress of one particular player or all players.
* **Elasticsearch Service**: The purpose of this service is to communicate with the Elasticsearch where all recorded events during the games are stored and obtain queried data. Microservice provides several endpoints to obtain different portions of data, e.g. events per one game or events per multiple games.
* **Sandbox Service**: Provides functionality to manage the lifecycle of sandboxes in the KYPO platform. It includes managing sandbox definitions, creating sandboxes, their removal, configuration, networking inside of sandboxes, or user configuration of machines. Description of sandbox topology can be found in section [Sandboxes](sandboxes/sandbox-topology/topology-definition)
* **OIDC Provider**: Service realized by OpenID Connect, which is used to authenticate the users logged into the KYPO platform, as well as to obtain basic profile information about the end-user in an interoperable and REST-like manner. It provides a secure authentication mechanism for microservices and protection of their APIs.
* **Angular Frontend**: User-friendly graphical user interface implemented using the Angular framework. Provides access to individual microservices and their selected functionalities via a web browser. 
* **Cloud service**: External service serves as a provider of hardware resources. Currently, the KYPO platform supports only the OpenStack cloud service.

!!! note
    The part of the KYPO which is responsible for catching, processing, and storing of events from training microservice or commands from machines in sandboxes is not displayed in the picture. Architecture of this part of platform is described in section [Logging](extras/logging/architecture.md).
