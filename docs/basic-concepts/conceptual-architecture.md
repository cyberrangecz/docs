We have designed the KYPO cyber range as a cloud platform for achieving maximum flexibility, scalability, and cost-effectiveness. A lot of development effort has been dedicated to user interactions within KYPO CRP, allowing us to offer access through a web browser. The following conceptual architecture displays the key architectural constructs in the designed system.

<p align="center" >
      <img style="width: 85%" src="../../img/basic-concepts/KYPO-portal-diagram.png">
</p>

### Cloud
The engine of the KYPO CRP environment is based on the cloud platform OpenStack. It controls large pools of computing, storage, and networking resources managed through APIs or a dashboard. It is mostly deployed as infrastructure-as-a-service in public and private clouds where virtual servers and other resources are made available to users.

### KYPO Portal
A graphical user interface for simple interaction of users with the KYPO CRP, easy access to sandboxes, and to the other functionalities. Represents the mediator between users and microservices that are running in the background. For more detailed information about microservices, see [Platform Components](../../installation-guide/platform-components/). 

### Git Repositories 
Git repositories are used to store created sandbox definitions by users. Then they are loaded by the respective microservice of KYPO Portal when needed to create a sandbox in the cloud. Access to the Git is configured during the KYPO CRP deployment. See [6. Configure access to the Gitlab repository](../../installation-guide/kypo-crp-deployment/#configure).

### Users  
Users have different roles with different scopes of work within KYPO CRP. They can create and manage trainings, manage other users, and they are also responsible for designing sandboxes via sandbox definitions. Users can access machines in the sandboxes using Spice client, Apache Guacamole remote desktop gateway, or directly using SSH.

