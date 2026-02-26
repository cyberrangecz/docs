We have designed the CyberRangeCZ Platform as a cloud platform for achieving maximum flexibility, scalability, and cost-effectiveness. A lot of development effort has been dedicated to user interactions within CyberRangeCZ Platform, allowing us to offer access through a web browser. The following conceptual architecture depicts the key architectural constructs in the designed system.

![Diagram of the conceptual architecture of the CyberRangeCZ Platform](/img/basic-concepts/portal-diagram.svg){ .center style="max-height: 420px;" }

### Git Repositories
Git repositories are used to store created sandbox definitions. They are loaded by the particular microservice of the CyberRangeCZ Platform portal, so they can be later used to create sandbox instances in the cloud. Access to Git is configured during the CyberRangeCZ Platform deployment.

### Users
Users have different roles with different scopes of work within CyberRangeCZ Platform. They can create and manage trainings, manage other users, and they are also responsible for designing sandboxes via sandbox definitions. Users can access machines in the cloud sandboxes using Apache Guacamole remote desktop gateway, or directly using SSH.

### CyberRangeCZ Platform Portal
A graphical user interface for simple interaction of users with the CyberRangeCZ Platform, easy access to cloud sandboxes, and to the other functionalities. Represents the mediator between users and microservices that are running in the background. For more detailed information about microservices, see [Platform Components](../installation-guide/platform-components.md).

### Cloud
The engine of the CyberRangeCZ Platform environment is based on the OpenStack and AWS cloud platforms. It controls large pools of computing, storage, and networking resources managed through APIs or a dashboard. It is mostly deployed as infrastructure-as-a-service in public and private clouds where virtual servers and other resources are made available to users.

