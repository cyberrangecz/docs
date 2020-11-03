Privileges and access rights of each KYPO user are determined by the **roles** appointed to their user [group](../../user-guide-basic/administration-agenda/groups.md).
All roles are imported into the KYPO portal by registering a [microservice](../../user-guide-basic/administration-agenda/microservices.md), where each microservice has exactly one default role. These roles are used slightly differently.

## How the Roles Are Used 
In the context of the KYPO CRP, we are using three abstract roles that are not part of any microservice. We have experienced that most of the users require the functionalities that are privileges of the specific set of [microservice roles](#microservice-roles). Each abstract role is composed of several roles of microservices that must be assigned to users by an administrator.

### Trainee
Each user who can log into the KYPO CRP automatically acquires this role. It is composed of the default roles of each microservice. For now, these roles are: ``ROLE_TRAINING_TRAINEE``, ``ROLE_USER_AND_GROUP_GUEST``, and ``ROLE_KYPO-SANDBOX-SERVICE_TRAINEE``.

### Instructor
The user who is responsible for creating exercises for trainees and for their management is called the instructor. Each instructor should have access to sandbox definitions, pools, cloud resources, training definitions, and training instances. Because of that, the instructor must have assigned the following roles: ``ROLE_TRAINING_ORGANIZER``, ``ROLE_TRAINING_DESIGNER``, ``ROLE_KYPO-SANDBOX-SERVICE_ORGANIZER``, and ``ROLE_KYPO-SANDBOX-SERVICE_DESIGNER``. The role of the trainee is assigned by default. 

### Administrator
User who is responsible for managing the whole KYPO CRP instance. The administrator must have assigned all the [microservice roles](#microservice-roles) described below. 

This is the preferable option to use the roles in the KYPO Platform. But it is possible to use bigger granularity by assigning only some roles of microservices. See the meaning of the individual roles in the next part of the page. 

!!! warning 
    The used concept of roles so far will be probably changed in the next release.


## Microservice Roles 

Current roles that are used in the KYPO portal can be divided into categories based on microservice that import them:

1. [Training roles](#training-roles)
2. [User and group roles](#user-and-group-roles)
3. [Sandbox roles](#sandbox-roles)

### Training Roles

``ROLE_TRAINING_TRAINEE``: **Trainees** are allowed to start, resume, and play the [training run](../../user-guide-basic/training-agenda/training-run.md). After the training is complete trainees can also check and compare their scores. The role of the trainee is the default role of each KYPO user.

``ROLE_TRAINING_ORGANIZER``: **Training organizers** can create and manage [training instances](../../user-guide-basic/training-agenda/training-instance.md), see the progress of trainees during the game, or see the results in form of graphs and tables. Each organizer can only access training instances in which they are set as an organizer.

``ROLE_TRAINING_DESIGNER``: **Training designers** can create and manage [training definitions](../../user-guide-basic/training-agenda/training-definition.md), that can be used to create training instances by the organizers. In a similar manner to the organizers, these users can only access training definitions that have them set as their designer.

``ROLE_TRAINING_ADMINISTRATOR``: **Training administrators** have all the privileges of the above roles with the exception being that they are not restricted by ownership of the training instances and definitions. This means that the training administrator can access all definitions and instances that exist on the KYPO platform.

### User and Group Roles

``ROLE_USER_AND_GROUP_GUEST``: **Guests** can only see information about himself or basic information about other users. It is the default role for every user of the KYPO platform.

``ROLE_USER_AND_GROUP_USER``: **Users** have at this moment the same access rights as the previous role **guest**.

``ROLE_USER_AND_GROUP_ADMINISTRATOR``: **Administrators** can fully access and manage users, groups, and microservices in the user and group agenda.

### Sandbox Roles

``ROLE_KYPO-SANDBOX-SERVICE_TRAINEE``: **Sandbox trainees** cannot access any part of the sandbox agenda, but they can access sandbox topology during the game. This role is the default role of all KYPO users.

``ROLE_KYPO-SANDBOX-SERVICE_ORGANIZER``: **Sandbox organizers** gain access to the management of the sandbox [pools](../../user-guide-basic/sandbox-agenda/pool.md). These pools contain sandboxes that are assigned to a specific trainee at the start of the game. 

``ROLE_KYPO-SANDBOX-SERVICE_DESIGNER``: **Sandbox designers** can create and manage [sandbox definitions](../../user-guide-basic/sandbox-agenda/sandbox-definition.md), that can be used by a sandbox organizer to create a pool of sandboxes. 

``ROLE_KYPO-SANDBOX-SERVICE_ADMIN``: **Sandbox admin** combines access rights of the above roles to grant full access to the sandbox agenda of the KYPO portal.
