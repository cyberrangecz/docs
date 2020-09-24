# Roles 

Privileges and access rights of each KYPO user are determined by the **roles** appointed to their user [group](./administration/group.md).
All roles are imported into KYPO portal by registering a [microservice](./administration/microservices.md). Current roles that are used in the KYPO portal can be 
divided between categories based on microservice that imported them:
1. [Training roles](#training-roles)
2. [User and group roles](#user-and-group-roles)
3. [Sandbox roles](#sandbox-roles)

## Training roles

``ROLE_TRAINING_TRAINEE``: **Trainees** are allowed to start, resume and play the [training run](./trainings/training-run.md). After the training is complete 
trainees can also check and compare their scores. Role of trainee is the default role of each KYPO platform user.

``ROLE_TRAINING_ORGANIZER``: **Training organizers** can create and manage [training instances](./trainings/training-instance.md). Each organizer  can only access
training instances in which they are set as organizer.

``ROLE_TRAINING_DESIGNER``: **Training designers** can create and manage [training definitions](./trainings/training-definition.md). 
In similar manner to the organizers, these users can only access training definitions that have them set as their designer.

``ROLE_TRAINING_ADMINISTRATOR``: **Training administrators** have all the privileges of the above roles with the exception being that
they are not restricted by ownership of the training instances and definitions. This means that training administrator can access all 
definitions and instances that exist on the KYPO platform.

## User and group roles

``ROLE_USER_AND_GROUP_GUEST``: **Guest** is the default role for every user of the KYPO platform and does not allow
any actions in the **User and Group** agenda.

``ROLE_USER_AND_GROUP_USER``: At this moment the **User** role has same access rights as the **Guest**.

``ROLE_USER_AND_GROUP_ADMINISTRATOR``: Users with the role **Administrator** can fully access and manage users, groups and microservices in 
the user and group agenda.

## Sandbox roles

``ROLE_KYPO-SANDBOX-SERVICE_TRAINEE``: Role of the **Sandbox trainee** is the default role of all KYPO users. Trainees
 cannot access any part of the sandbox agenda.

``ROLE_KYPO-SANDBOX-SERVICE_DESIGNER``: Role of the **Sandbox designer** allows the user to create and manage 
[sandbox definitions](./sandboxes/sandbox-definition.md).

``ROLE_KYPO-SANDBOX-SERVICE_ORGANIZER``: Role of the **Sandbox organizer** grants access to the management of the sandbox 
[pools](./sandboxes/pool.md).

``ROLE_KYPO-SANDBOX-SERVICE_ADMIN``: **Sandbox admin** combines access rights of the above roles to grant the full access to the
sandbox agenda of the KYPO portal.