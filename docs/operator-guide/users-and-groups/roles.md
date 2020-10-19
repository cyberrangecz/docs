## Roles 

Privileges and access rights of each KYPO user are determined by the **roles** appointed to their user [group](../../user-guide/administration.md#group-overview).
All roles are imported into the KYPO portal by registering a [microservice](../../user-guide/administration.md#microservice-registration), where each microservice has exactly one default role. Current roles that are used in the KYPO portal can be divided into categories based on microservice that register them:
1. [Training roles](#training-roles)
2. [User and group roles](#user-and-group-roles)
3. [Sandbox roles](#sandbox-roles)

These roles are then internally used by individual microservices to restrict access to their functionalities.

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


## Tables of permissions
The following tables display the actions that can perform the users with the specified role. To be specific it displays all endpoints available across KYPO microservices that can be called. Because of that tables are divided based on individual microservices and then divided based on the resource to which they relate. The more detailed description of the endpoints are int API section of this documentation. 


### User and Group microservice


#### Users endpoints  
| Action | CRUD operation |  Guest | User | Administrator |
| ------ | :------------: |  :---: | :--: | :-----------: |
| Get users | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users In Groups | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get user | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get all users not in given group | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get roles of user | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get user info | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get users with given IDs | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete user | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete users | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Groups endpoints
| Action | CRUD operation | Guest | User | Administrator |
| ------ | :------------: | :---: | :--: | :-----------: |
| Create new group | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get groups | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get group | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get roles of group | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Update group | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Remove users | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Assign role to group | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Remove role from group | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Add users | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete group | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete groups | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Roles endpoints
| Action | CRUD operation | Guest | User | Administrator |
| ------ | :------------: | :---: | :--: | :-----------: |
| Get roles | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get role | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users with given role | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users with given role type | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get users with given role type and not with given IDs | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |

#### Microservices endpoints
| Action | CRUD operation | Guest | User | Administrator |
| ------ | :------------: | :---: | :--: | :-----------: |
| Get Microservices | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Register New Microservice | CREATE/UPDATE | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |

!!! warning
    Registration of a microservice is not secured at all.

### Training microservice 

#### Training Definitions endpoints
!!! note
    The symbol :material-hexagram:{: .green } means that action can be performed only by the designer of that particular training definition.


| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create training definition  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Clone training definition  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Create level  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Find training definition by ID  | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Find all training definitions | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Find level by ID | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get designers | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get organizers | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get designers not in given training definition | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get beta testers | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green }| :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get authors | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Find all training definitions for  organizers | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Update training definition | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Swap levels | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Move level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update game level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update info level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update assessment level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Edit authors | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Switch state | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete training definition | DELETE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Delete one level | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |


#### Training Instances endpoints

!!! note
    The symbol :material-hexagram:{: .green } means that action can be performed only by the organizer of that particular training instance.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create training instance | CREATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find training instance by ID  | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find all training instances | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find all training runs by training instance ID | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get organizers of training instance | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } |:material-check-bold:{: .icon .green } |
| Get organizers not in given training instance | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } |:material-check-bold:{: .icon .green } |
| Update training instance | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Assign pool | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Unassign pool | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Edit organizers | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training instance | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Training Runs endpoints
!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training run.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Access training run | CREATE |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find training run by ID  | READ | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find all training runs | READ |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get all accessed training runs | READ |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get next level | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get solution | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get hint | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Resume training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get participant | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Finish training run | UPDATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Is correct flag | UPDATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Evaluate responses to assessment | UPDATE | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Archive training run | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training runs | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training run | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Export & Import endpoints

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Import training definition | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get exported training definition and levels | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Archive training instance | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Visualizations endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training instance.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Gather visualization info for training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Gather visualization info for training instance | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get participants for given training instance| READ | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users by IDs| READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |


### Sandbox microservice 
