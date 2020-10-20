# Administration 
That administration agenda is available only for KYPO portal users with the role of `ROLE_USER_AND_GROUP_ADMINISTRATOR`. This agenda is used for assigning roles (e.g., designer, organizer, or administrator) to the other users to be able to work in the KYPO portal as expected. By default, all the logged-in users are assigned to `DEFAULT-GROUP` that contains all the basic roles that are essential to play a game (for that reason it is not required to do some extra step for students that enroll in the class for playing a game in KYPO portal).
An administrator can access one of the following pages: 

* [User Overview](#user-overview), 
* [Group Overview](#group-overview),
* [Microservice Registration](#microservice-registration), 

by clicking a particular button on the front page of the KYPO Portal:

<p align="center">
  <img src="../../img/user-guide/administration/administration-agenda.png">
</p>


or by clicking the button in the left panel in the section Administration:

<p align="center">
  <img src="../../img/user-guide/administration/administration-left-panel.png">
</p>


## User Overview 
The page is used to list all users that had logged into the KYPO platform using arbitrary OIDC Provider (MUNI, KYPO, ...). In the following table, each row represents one user. An administrator can view their roles by clicking the expand button :material-chevron-down:{: .grey .icon } (next to the name of the user) that expands the row with the list of roles of a particular user. One user can be deleted by clicking on delete button :material-delete:{: .red .icon } or multiple users can be deleted by checking users with checkboxes situated on the left side of the row and clicking the ![delete-button](../img/buttons/big-delete-button.png) button.  

![user-overview](../img/user-guide/administration/users-overview.png)

## Group Overview 
The page is used to list all groups created in the KYPO platform. Groups are important because roles are not assigned to users but to groups. The user acquires access to the KYPO portal agendas based on the roles of the groups they belong to.

![group-overview](../img/user-guide/administration/group-overview.png) 

To create a new group, the administrator must click on ![create-button](../img/buttons/create-button.png) button that redirects him to the page [Create Group](#create-or-edit-group). The last column of the table contains actions :material-pencil:{: .icon .blue } &nbsp; :material-delete:{: .red .icon }: 


??? pencil "Edit"
    
    Click the button will redirect to [Edit Group](#create-or-edit-group) page.
    
??? trash-can "Delete"
    
    Click the button, the following confirmation window will be opened: 
    
    <p align="center">
      <img src="../../img/user-guide/administration/delete-confirmation.png">
    </p>
    
    After confirming, the group will be deleted from the KYPO portal.
    
    !!! info
        Multiple groups can be deleted by checking groups with checkboxes situated on the left side of the table row and by clicking on ![delete-button](../img/buttons/big-delete-button.png) button.


### Create or Edit Group

The page consists of three panels:

[1. Create/Edit Group](#1-createedit-group) 
[2. Edit members](#2-edit-members) 
[3. Edit roles](#3-edit-roles) 

![create-group](../img/user-guide/administration/create-group-all.png)

!!! note 
    Create Group and Edit Group pages are same but Edit Group page has some fields pre-filled. 

During the creation of a group, the second and third panels are disabled. To make them accessible, the administrator must fill the required fields in the first panel and either click on: 

1. ![create-button](../img/buttons/create-button.png) that will create the new group and redirect the administrator back to [Group Overview](#group-overview).
2. ![create-and-edit-button](../img/buttons/create-and-continue-button.png) that will stay on the page and allow the administrator to edit **members** and **roles** of the group.

#### 1. Create/Edit Group
Here, the administrator is required to fill up all the necessary fields before creating a new group. The `Expiration Date` field is optional and is useful in the cases when the administrator will create a group of designers, e.g., for a particular semester. After filling up fields, click on the ![create-button](../img/buttons/create-button.png) button to save the group. Then panels **Edit members** and **Edit roles** will be rolled down. 

![create-group-panel](../img/user-guide/administration/create-group.png)
#### 2. Edit members
Here, the administrator can add users individually or import all users from the group. The part **Add users** provide an easy way to search for users whose administrator would like to add to the group. Administrators can also add all users from the specific group in the part **Import users**. Click on the ![add-button](../img/buttons/add-button.png) button to add selected users to the group. All users will be added to the group and will be present in the list in the part **Members of group**. A user or multiple users can be removed via the common way mentioned before.

![edit-members-panel](../img/user-guide/administration/edit-members.png)
#### 3. Edit roles 
Here, the administrator can assign roles to the group. The part **Add roles** provide an easy way to search for roles which the administrator would like to assign to the group. Click on the ![add-button](../img/buttons/add-button.png) button to assign all selected roles to the group. Assigned roles will be present in the list in the part **Roles of group**. A role or multiple roles can be removed via the common way mentioned before.

![edit-roles-panel](../img/user-guide/administration/edit-roles.png)
## Microservice Registration
This page is used to register a new microservice which is then used in the background of the platform. The recommended way is to import the [kypo2-security-commons library](https://gitlab.ics.muni.cz/kypo-crp/backend-java/kypo2-security-commons) into service and register microservice during startup.

![microservice-page](../img/user-guide/administration/microservice-registration.png)
