We have designed the KYPO cyber range as a cloud platform for achieving maximum flexibility, scalability, and cost-effectiveness. A lot of development effort has been dedicated to user interactions within KYPO CRP, allowing us to offer access through a web browser. The following conceptual architecture depicts the key architectural constructs in the designed system.

<p align="center" >
      <img style="width: 85%" src="../../img/basic-concepts/KYPO-portal-diagram.png">
</p>

### Git Repositories 
Git repositories are used to store created sandbox definitions that can be used in a cloud environment, local environment, or both. In both cases, they are loaded by the particular microservice of the KYPO portal, so they can be later used to create sandbox instances in the cloud or display the topology of local sandboxes. Access to Git is configured during the KYPO CRP deployment. See [6. Configure access to the Gitlab repository](../../installation-guide/kypo-crp-deployment/#configure).

### Users  
Users have different roles with different scopes of work within KYPO CRP. They can create and manage trainings, manage other users, and they are also responsible for designing sandboxes via sandbox definitions. Users can access machines in the cloud sandboxes using Spice client, Apache Guacamole remote desktop gateway, or directly using SSH. On the other hand users can access local sandboxes directly using the vagrant specific command.

### KYPO Portal
A graphical user interface for simple interaction of users with the KYPO CRP, easy access to cloud sandboxes, and to the other functionalities. Represents the mediator between users and microservices that are running in the background. For more detailed information about microservices, see [Platform Components](../../installation-guide/platform-components/). 

### Cloud
The engine of the KYPO CRP environment is mostly based on the OpenStack cloud platform. It controls large pools of computing, storage, and networking resources managed through APIs or a dashboard. It is mostly deployed as infrastructure-as-a-service in public and private clouds where virtual servers and other resources are made available to users.

### User Computer
As an alternative to cloud sandboxes, the local sandboxes can be built at the user's computer using VirtualBox and Vagrant. It saves cloud resources and allows creating trainings with a large number of users with only small differences. It requires interaction of the user who must clone the sandbox definition repository and run a command to build a sandbox. Also, the user's computer must meet hardware and virtualization requirements. 
