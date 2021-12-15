The following tables display the actions that can perform the users with the specified role. To be specific it displays all endpoints available across KYPO microservices that can be called. Because of that tables are divided based on individual microservices and then divided based on the resource to which they relate. The more detailed description of the endpoints are in the pages in this section. 


### User and Group Microservice


#### Users Endpoints  
| Action | CRUD operation |  Guest | User | Administrator |
| ------ | :------------: |  :---: | :--: | :-----------: |
| Get users | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users In groups | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get user | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get all users not in given group | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get roles of user | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get user info | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get users with given IDs | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete user | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete users | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Groups Endpoints
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

#### Roles Endpoints
| Action | CRUD operation | Guest | User | Administrator |
| ------ | :------------: | :---: | :--: | :-----------: |
| Get roles | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get role | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users with given role | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users with given role type | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get users with given role type and not with given IDs | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |

#### Microservices Endpoints
| Action | CRUD operation | Guest | User | Administrator |
| ------ | :------------: | :---: | :--: | :-----------: |
| Get Microservices | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Register New Microservice | CREATE/UPDATE | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |

!!! warning
    Registration of a microservice is not secured at all.

### Training Microservice 

#### Linear Training Definitions Endpoints

!!! note
    The symbol :material-hexagram:{: .green } means that action can be performed only by the designer of that particular training definition.


| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create training definition  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
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
| Update multiple levels | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update training level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update info level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update assessment level | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Edit authors | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Switch state | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete training definition | DELETE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Delete one level | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |


#### Linear Training Instances Endpoints

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

#### Linear Training Runs Endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training run.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Access training run | CREATE |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Is correct answer | CREATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find training run by ID  | READ | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Find all training runs | READ |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get all accessed training runs | READ |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get next level | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get correct answers of training run | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get solution | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get hint | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Resume training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get participant | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Finish training run | UPDATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Evaluate responses to assessment | UPDATE | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Archive training run | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training runs | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training run | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Export & Import Endpoints

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Import training definition | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get exported training definition and levels | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Archive training instance | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Visualizations Endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training instance.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Gather visualization info for training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Gather visualization info for training instance | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get clustering visualization dat for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get table visualization dat for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get timeline visualization dat for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get progress visualization dat for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get level tabs visualization dat for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get participants for given training instance| READ | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get commands in training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get clustering visualization data for trainee | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get table visualization data for trainee | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get timeline visualization data for trainee | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get users by IDs| READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |

### Adaptive Training Microservice 

#### Adaptive Training Definitions Endpoints

!!! note
    The symbol :material-hexagram:{: .green } means that action can be performed only by the designer of that particular training definition.


| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create training definition  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Clone training definition  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get training definition by ID  | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get all training definitions | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get designers | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get organizers | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get designers not in given training definition | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get authors | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Find all training definitions for  organizers | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Update training definition | UPDATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Edit authors | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Switch state | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete training definition | DELETE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |

#### Phases Endpoints

!!! note
    The symbol :material-hexagram:{: .green } means that action can be performed only by the designer of that particular training definition.


| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create phase  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Get phase by ID | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Get phases by training definition ID | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Move phase | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update training phase | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update info phase | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Update questionnaire phase | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Delete phase | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |

#### Tasks Endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the designer of that particular training phase.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the designer of that particular task.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create task in phase  | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Clone task | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-check-bold:{: .icon .green } |
| Get task by ID | READ | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-check-bold:{: .icon .green } |
| Move task | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-check-bold:{: .icon .green } |
| Update task | UPDATE |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-check-bold:{: .icon .green } |
| Delete task | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-check-bold:{: .icon .green } |

#### Adaptive Training Instances Endpoints

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

#### Adaptive Training Runs Endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training run.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Access training run | CREATE |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Is correct answer | CREATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get training run by ID  | READ | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get all training runs | READ |  :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get all accessed training runs | READ |  :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get next phase | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get solution | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Resume training run | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get participant | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Finish training run | UPDATE | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Evaluate responses to questionnaire | UPDATE | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Archive training run | UPDATE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training runs | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete training run | DELETE |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Export & Import Endpoints

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Import training definition | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Get exported training definition and phases | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Archive training instance | READ |  :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Visualizations Endpoints

!!! note
    The symbols: 
    &nbsp; &nbsp; &nbsp; &nbsp; :material-hexagram:{: .green } means that action can be performed only by the trainee of that particular training run.
    &nbsp; &nbsp; &nbsp; &nbsp; :material-cards-spade:{: .green } means that action can be performed only by the organizer of that particular training run.

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Get Sankey diagram data | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get transition graph data for organizer | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } :material-cards-spade:{: .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get transition graph data for trainee | READ | :material-check-bold:{: .icon .green } :material-hexagram:{: .green } | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

### Sandbox Microservice 

#### Pools Endpoints

| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create sandbox allocation unit| CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Lock given pool | CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Create new pool | CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Create cleanup requests | CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get a list of Sandbox Allocation Units | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| List locks for given pool | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| List Allocation Request for this pool | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get lock of the given pool | READ | :material-close-thick:{: .icon .red }| :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve the definition associated with a pool | READ | :material-close-thick:{: .icon .red }| :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get a list of pools | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| List Cleanup Request for this pool | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get unlocked sandbox in given pool and lock it | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get a list of sandboxes in given pool | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Generate SSH config for User access to this sandbox | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a pool | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete all Sandbox Allocation Units in pool | DELETE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete given lock | DELETE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete pool | DELETE | :material-close-thick:{: .icon .red }  | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Cleanup Requests Endpoints
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Retrieve a Sandbox Provisioning Cleanup stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Networking Cleanup stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Cleanup Request | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve an openstack Cleanup stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Cancel given Cleanup Request | UPDATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Cloud Endpoints 
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Get list of images | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Networking Cleanup stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get the quota set and name of project | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |


#### Definitions Endpoints
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create a new sandbox definition | CREATE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Retrieve the definition | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Retrieve a list of sandbox definitions | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green }| :material-check-bold:{: .icon .green } |
| Retrieve a list of definition refs (branches and tags) | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |
| Delete the definition | DELETE | :material-close-thick:{: .icon .red } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } |


#### Allocation Requests Endpoints
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| List sandbox Resources | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Networking Allocation stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a list of Ansible Outputs | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Provisioning Allocation stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Allocation Request | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| List sandbox Events | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a list of Ansible Outputs | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve an openstack allocation stage | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Cancel given Allocation Request | UPDATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |



#### Sandbox Allocation Units Endpoints
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Create cleanup request | CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Allocation Unit | READ | :material-close-thick:{: .icon .red }| :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Cleanup Request for an Allocation Unit. | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a Sandbox Allocation Request for an Allocation Unit | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete cleanup request | DELETE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

#### Sandboxes Endpoints
| Action | CRUD operation | Trainee | Organizer | Designer | Administrator | 
| ------ | :------------: | :-----: | :-------: | :------: | :-----------: |
| Lock given sandbox | CREATE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get Spice consoles urls | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get MAN out port IP | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| List locks for given sandbox | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get topology data for given sandbox | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Generate SSH config for User access to this sandbox | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get a console for given machine | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Get lock of given sandbox | READ | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a sandbox | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Retrieve a VM info | READ | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Perform specified action on given VM | UPDATE | :material-check-bold:{: .icon .green } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |
| Delete given lock | DELETE | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } | :material-close-thick:{: .icon .red } | :material-check-bold:{: .icon .green } |

