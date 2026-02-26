Users' roles restrict privileges and access rights to pages in the CyberRangeCZ Platform portal, resources in microservices, or the possibility of specific actions. CyberRangeCZ Platform has a permission system with fine-grained control over what users can see and do. All of this is managed through the **User And Group microservice** and **OIDC Provider**.

When accessing the CyberRangeCZ Platform portal, users are asked to log in via the OIDC Provider. After successful login, an access token is obtained from OIDC Provider, and User And Group microservice determine the roles of the user. That information is stored and available during the whole session.

!!! note
    Refresh the CyberRangeCZ Platform Portal page to apply changes in the roles of the user that have been made by an administrator.

The permission system is based on relations between four types of entities (Users, Groups,  Roles, and Microservices)
.

![permission-system](/img/user-guide-advanced/users-and-groups/permission-system.svg)

A **user** can be part of **one or more** groups. Each user is part of the special **default group**.

**Groups** have assigned **one or more** roles. The above-mentioned default group has assigned each role that is marked as default.

**Roles** are part of the individual **microservices**. They are internally used by microservices to restrict access to their functionalities. Roles are imported into the CyberRangeCZ Platform by registering a [microservice](../../user-guide-basic/administration-agenda/microservices.md), where each microservice has exactly one default role.

The users' roles are determined based on the groups they are assigned to and roles appointed to these groups. The overview of the roles and rights they provide are on the [next page](roles.md).
