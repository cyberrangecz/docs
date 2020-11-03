# Overview

The objective of the **User guide** is to provide a basic guidelines to the users of the KYPO Portal. KYPO Portal is a graphical user interface that mediates access to the platform for the end-users by providing them with interactive visual tools. In particular, the portal is designed to cover the microservices that manage the different areas of the KYPO platform that provide core functionalities.

The portal is divided into three **KYPO agendas** and user guide functions as a manual on how to operate all of the functions that these agendas offer.

## User Roles

Access to KYPO Portal depends a lot on the role you hold as a user. There are three main roles we differentiated and depending on them you can access different pages and perform various functionalities in the KYPO Portal.

* **Trainees:** Everybody who has access to the KYPO Portal and is interested in participating in the training can perform actions inside of the [Traning run](../training-agenda/training-run).
* **Instructors:** Users who are responsible for preparing and creating trainings and corresponding sandboxes can access the following pages: 
    * [Training definitions](../training-agenda/training-definition) and [Training instances](../training-agenda/training-instance) for overview and management of trainings. 
    * [Sandbox definitions](../sandbox-agenda/sandbox-definition) and [Sandbox pools](../sandbox-agenda/pool) needed for management of sandboxes, and [Resources](../sandbox-agenda/resources) for cloud resources overview.
* **Administrators:** Users who are responsible for managing the whole KYPO CRP instance. They have access to every above-mentioned page in the KYPO Portal. Moreover, they can also have rights to manage entities like users, groups, and microservices in [Administration Agenda](../administration-agenda/administration-agenda-overview). 

!!! note
    To better understand the meaning of the roles, see the chapter [Users and Groups](../../user-guide-advanced/users-and-groups/roles).


## KYPO Portal Home Page

After a successful login, the home page of the KYPO Portal contains the elements marked in the following picture. 

!!! warning "Trainee"
    A trainee cannot see the home page. See [The Trainee's Point of View](#the-trainees-point-of-view).

![KYPO-home-page](../img/user-guide-basic/KYPO-home-page.png)


**Global navigation:** A persistent navigation menu, displayed on all pages. The menu is divided based on the agendas and contains links to concrete pages.
**User menu:** User-specific information such as name and e-mail, and a logout button.
**Breadcrumbs:** Full path to the current page. Represents the folder structure.
**Notifications:** The list of the latest notifications.
**Agendas:**

 1. **[Trainings agenda](./training-agenda/training-agenda-overview.md)** with main focus on creation and organization of trainings.
 2. **[Sandboxes agenda](./sandbox-agenda/sandbox-agenda-overview.md)** specifies guidelines for sandbox creation and realization. 
 3. **[Administration agenda](./administration-agenda/administration-agenda-overview.md)** deals with the administration of users and their access to the specific parts of the KYPO Portal based on user access roles.

### The Trainee's Point of View
Each trainee will be after a successful log-in directly redirected to the [Training Run Overview](../training-agenda/training-run/#training-runs-overview) page. 

![KYPO-home-page-trainee](../img/user-guide-basic/KYPO-home-page-trainee.png)


### The Instructor's Point of View
The instructor can access both Trainings Agenda and Sandboxes Agenda. 

![KYPO-home-page-trainee](../img/user-guide-basic/KYPO-home-page-instructor.png)

### The Administrator's Point of View 

An administrator can access any page. 

![KYPO-home-page-admin](../img/user-guide-basic/KYPO-home-page-admin.png)

