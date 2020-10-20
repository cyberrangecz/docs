# Training definition

Users with the role `ROLE_TRAINING_DESIGNER` can use the training agenda to create and manage training definitions. A designer can access the page [Training Definition Overview](#training-definition-overview) by clicking the **Training Definition** button on the front page of KYPO Portal:

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-agenda-button.png">
</p>

or by clicking the **Definition** button in the left panel in the section Trainings.

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-sidebar.png">
</p>

## Training Definition Overview
This page lists all definitions that are available to the designer (the designers can see only the ones that they create or the ones that they are co-authors). In the top right corner are located buttons ![create-button](../../img/buttons/create-button.png) and ![upload-button](../../img/buttons/upload-button.png) that are used to [add a new definition](#add-a-new-definition) into the KYPO portal. In the following table, each row represents one training definition. The last column of this table contains actions :material-pencil:{: .blue .icon} &nbsp; :material-delete:{: .red .icon} &nbsp; :material-dots-vertical:{: .grey .icon} that can be executed on a given training definition.

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-overview.png">
</p>

!!! info
    Users with the role `ROLE_TRAINING_ADMINISTRATOR` are able to see all of the training definitions.

??? pencil "Edit"
    
    Click the button, the training definition editor page will be opened:
    
    <p align="center">
        <img src="../../../img/kypo-portal/trainings/training-definition/TD-edit-panel.png">
    </p>
    
    Here the designer can use given panels to edit a training definition in the same fashion as when they are [creating a new definition](#1-create-a-new-definition). Every change needs to be saved with the ![save](../../img/buttons/save-button.png) button. 
    
    !!! info
        The designer can only save changes made in the training definition that is **Unreleased**. **Released** and **Archived** definitions cannot be changed.
    
??? trash-can "Delete"
    
    Click the button, the following confirmation window will be opened: 
    
    <p align="center">
      <img src="../../../img/user-guide/training-agenda/training-definition/TD-delete-panel.png">
    </p>
    
    After confirming, the given training definition will be deleted from the KYPO portal.
    
    !!! info
        Training definitions that are used in any **training instance** cannot be deleted. 

??? clone "Clone"
    
    Click the button, the following window will be opened:
    
    <p align="center">
      <img src="../../../img/kypo-portal/trainings/training-definition/TD-clone-panel.png">
    </p>
    
    Here the designer can change the name of the new training definition that will be added into the KYPO portal. The contents of this new definition will be identical to the original training definition.
    
??? download "Download"
    
    Click the button to export the respective training definition as a file in JSON format that can be downloaded into the local machine. This file can be used to [upload](#2-upload-a-definition-from-json-file) a given definition back into the KYPO portal. 
    
??? preview "Preview"
   
    Click the button to show how the training definition will look from the perspective of the trainee.
    
    <p align="center">
      <img src="../../../img/user-guide/training-agenda/training-definition/TD-preview.png">
    </p>
    
    !!! info
        Sandbox topologies in the preview are mocked and not connected to any real sandbox so they cannot be used to access any virtual network.
    
??? lock "Release"
   
    Click the button to change the state of the definition to **Released**. 
    Released definitions cannot have their content changed but they can have its state changed to either **Unreleased** or **Archived**.

  
??? unlock "Unrelease"
    
    Click the button to change the state of the definition to **Unreleased**.
    Unreleased definitions allow the designer to edit the content inside of them and can have its state changed to **Released**.
    
??? archive "Archive"
    
    Click the button to change the state of the definition to **Archived**.
    Archived definitions cannot have their content changed and cannot be switched to any other state.

----------------------------------------------------

!!! note
    Actions 3. - 8. can be accessed in the menu shown after clicking on the **more options** button :material-dots-vertical:{: .grey .icon}. 

## Add a new definition
There are three approaches on how to create a new training definition in the KYPO Portal:

1.  [**Create a new definition from a scratch**](#1-create-a-new-definition) 
2.  [**Upload a definition from JSON file**](#2-upload-a-definition-from-json-file)
3.  Clone an existing definition (more in the previous [**subsection**](#training-definition-overview))

### 1. Create a new definition
To create a new training definition click on the top right button ![Create-button](../../img/buttons/create-button.png). This will open the training definition editor page.

#### Create Training Definition panel
In the first panel of the training definition editor, the designer can edit fields that describe the new definition. When the designer is done they can either click on:
1.  ![Create-button](../../img/buttons/create-button.png) that will create a new definition and redirect them back to [Training Definition Overview](#training-definition-overview).
2.  ![Create-and-continue](../../img/buttons/create-and-continue-button.png) that will allow the designer to edit **authors** and **levels** of the definition.

<p align="center">
    <img src="../../../img/user-guide/training-agenda/training-definition/TD-create-panel.png">
</p>

#### Edit Authors panel
In the second panel of training definition editor, the designer can add and remove authors from this definition.

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-edit-authors.png">
</p>

#### Edit Levels panel
In the third panel the designer can add, delete, and edit game levels of the training definition.

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-edit-levels.png">
</p>

To add a new level the designer can click ![Add-button](../../img/buttons/add-button.png) that will roll down a menu in which the designer can choose a type of the new level:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-levels.png">
</p>

!!! tip
    To change the order of levels, use drag-and-drop mechanism. Select a level in level bar by "grabbing" it and dragging it to a different position.

##### I. Game level
At the game level, a player can access a virtual network inside the sandbox to find a solution to the problem assigned by level content. The designer can fill this form to specify details of the new level (when the designer is done editing level they must save changes with the ![save](../../img/buttons/save-button.png) button.

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-GL-panel.png">
</p>

Under the game level editing form, there is a fourth additional panel that the designer can use to create, delete and, edit **hints** that are associated with a given game level.

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-hint-panel.png">
</p>

A new hint can be added with the ![add-button](../../img/buttons/add-button.png) button and edited with the following form (when the designers finish the editing of hints they must save changes with the ![save](../../img/buttons/save-button.png) button). To change the order of hints use the drag-and-drop mechanism. 

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-hint-edit.png">
</p>

##### II. Assessment level
In the assessment level, the players answer a list of questions. Content of this level can be edited with the following form (when the designers finish the editing of this level they must save changes with the ![save](../../img/buttons/save-button.png) button:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-AL-panel.png">
</p>

Under the assessment level editing form there is an additional **Questions** panel to create, delete and, edit questions associated with the given assessment level:   
 
<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-questions-panel.png">
</p>

The designer can choose to create a test or questionnaire, so the creation of the question may differ based on the type of assessment. A new question can be added with the ![add-button](../../img/buttons/add-button.png) button that will roll down the menu where the designer can choose a type of the new question:

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-question.png">
</p>

Each type has its specific editing form (when the designers finish the questions they must save changes with the ![save](../../img/buttons/save-button.png) button):

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-questions-edit.png">
</p>

##### III. Info Level
In the info level the player can only read content specified by the designer in the following form:

<p align="center">
  <img src="../../../img/user-guide/training-agenda/training-definition/TD-IL-panel.png">
</p>


### 2. Upload a definition from JSON file
To upload a training definition the designer can click in the **Training Definition Overview** on the top right ![upload-button](../../img/buttons/upload-button.png) button. This will open the following window:

<p align="center">
  <img src="../../../img/user-guide/training-agendas/training-definition/TD-upload-panel.png">
</p>


The designer can upload training definitions that were stored in the JSON file. This use-case is useful in the situation when the designer wants to re-use the training definition stored in the past.
