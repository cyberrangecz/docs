## Roles 

Privileges and access rights of each KYPO user are determined by the **roles** appointed to their user [group](../../user-guide/administration-agenda/groups.md).
All roles are imported into the KYPO portal by registering a [microservice](../../user-guide/administration-agenda/microservices.md), where each microservice has exactly one default role. Current roles that are used in the KYPO portal can be divided into categories based on microservice that import them:

1. [Training roles](#training-roles)
2. [User and group roles](#user-and-group-roles)
3. [Sandbox roles](#sandbox-roles)

### Training roles

``ROLE_TRAINING_TRAINEE``: **Trainees** are allowed to start, resume and play the [training run](../../user-guide/training-agenda/training-run.md). After the training is complete trainees can also check and compare their scores. The role of the trainee is the default role of each KYPO user.

``ROLE_TRAINING_ORGANIZER``: **Training organizers** can create and manage [training instances](../../user-guide/training-agenda/training-instance.md), see the progress of trainees during the game, or see the results in form of graphs and tables. Each organizer can only access training instances in which they are set as an organizer.

``ROLE_TRAINING_DESIGNER``: **Training designers** can create and manage [training definitions](../../user-guide/training-agenda/training-definition.md), that can be used to create training instances by organizers. In a similar manner to the organizers, these users can only access training definitions that have them set as their designer.

``ROLE_TRAINING_ADMINISTRATOR``: **Training administrators** have all the privileges of the above roles with the exception being that they are not restricted by ownership of the training instances and definitions. This means that the training administrator can access all definitions and instances that exist on the KYPO platform.

### User and group roles

``ROLE_USER_AND_GROUP_GUEST``: **Guest** can only see information about himself or basic information about other users. It is the default role for every user of the KYPO platform.

``ROLE_USER_AND_GROUP_USER``: **User** has at this moment the same access rights as the previous role **guest**.

``ROLE_USER_AND_GROUP_ADMINISTRATOR``: **Administrators** can fully access and manage users, groups, and microservices in the user and group agenda.

### Sandbox roles

``ROLE_KYPO-SANDBOX-SERVICE_TRAINEE``: **Sandbox trainees** cannot access any part of the sandbox agenda, but they can access sandbox topology during the game. This role is the default role of all KYPO users.

``ROLE_KYPO-SANDBOX-SERVICE_ORGANIZER``: **Sandbox organizers** gains access to the management of the sandbox [pools](../../user-guide/sandbox-agenda/pool.md). These pools contain sandboxes that are assigned to specific trainee at the start of the game. 

``ROLE_KYPO-SANDBOX-SERVICE_DESIGNER``: **Sandbox designers** can create and manage [sandbox definitions](../../user-guide/sandbox-agenda/sandbox-definition.md), that can be used by sandbox organizer to create pool of sandboxes. 

``ROLE_KYPO-SANDBOX-SERVICE_ADMIN``: **Sandbox admin** combines access rights of the above roles to grant full access to the sandbox agenda of the KYPO portal.
