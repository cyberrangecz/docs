# Training definition

Training designers can use training definition agenda to create and manage training definitions. A designer can access [Training Definition Overview](#training-definition-overview) by clicking the `Training Definition` button on the front page of KYPO Portal:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-agenda-button.png">
</p>

## Training Definition Overview
The page lists all definitions that are available to the designer (the designers can see only the ones that they create or the ones that they are co-authors). In the top right corner are located buttons ![create-button](../../img/buttons/create-button.png) ![upload-button](../../img/buttons/upload-button.png) that are used to [add a new definition](#add-a-new-definition) into KYPO portal. In the following table, each row represents one training definition. The last column of this table contains [actions](#actions) :material-pencil:{: .blue .icon} &nbsp; :material-delete:{: .red .icon} &nbsp; :material-dots-vertical:{: .grey .icon} that can be executed on a given training definition.

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-overview.png">
</p>

!!! note
    Users with the administrator role are able to see all of the training definitions.

??? pencil "Edit"
    
    If the designer clicks the **edit** button, the training definition editor page will be opened:
    
    <p align="center">
        <img src="../../../img/kypo-portal/trainings/training-definition/TD-edit-panel.png">
    </p>
    
    Here the designer can use given panels to edit training definition in the same fashion as when they are [creating new definition](#1-create-a-new-definition). Every change needs to be saved with ![save](../../img/buttons/save-button.png) button. 
    
    !!! note
        the designer can only save changes made in training definition that is *Unreleased*. *Released* and *Archived* definitions cannot be changed.
    
??? trash-can "Delete"
    
    If the designer clicks the **delete** button, following confirmation window will be opened: 
    
    <p align="center">
      <img src="../../../img/kypo-portal/trainings/training-definition/TD-delete-panel.png">
    </p>
    
    After confirming, the given training definition will be deleted from the KYPO portal.
    
    !!! note
        Training definitions that are used in any **training instance** cannot be deleted. 

??? clone "Clone"
    
    If the designer clicks the **clone** button, following window will be opened:
    
    <p align="center">
      <img src="../../../img/kypo-portal/trainings/training-definition/TD-clone-panel.png">
    </p>
    
    Here the designer can change the name of the new training definition that will be added into the KYPO portal. The contents of this new definition will be identical to the original training definition.
    
??? download "Download"
    
    If the designer clicks the **download** button, the given training definition will be stored into a JSON file that can be downloaded into the local machine. This file can be used to [upload](#2-upload-a-definition-from-json-format) given definition back into KYPO portal. 
    
??? preview "Preview"
   
    If the designer clicks the **preview** button, they will be shown how the training definition will look from the perspective of the trainee:
    
    <p align="center">
      <img src="../../../img/kypo-portal/trainings/training-definition/TD-preview.png">
    </p>
    
    !!! note
        sandbox topologies in the preview mocked and not connected to any real sandbox so they cannot be used to access any virtual network.
    
??? lock "Release"
   
    If the designer clicks the **release** button the state of the definition will be changed to **Released**. 
    **Released** definitions cannot have their content changed but they can have its state changed to either **Unreleased** or **Archived**.

  
??? unlock "Unrelease"
    
    If the designer clicks the **unrelease** button the state of the definition will be changed to **Unreleased**.
    **Unreleased** definitions allow the designer to edit the content inside of them and can have its state changed to **Released**.
    
??? archive "Archive"
    
    If the designer clicks the **archive** button the state of the definition will be changed to **Archived**.
    **Archived** definitions cannot have their content changed and cannot be switched to any other state.

!!! note
    actions 3. - 8. can be accessed in menu shown after clicking on the *more options* :material-dots-vertical:{: .grey .icon} button. 

## Add a new definition
There are three approaches how to create a new training definition in KYPO Portal:
1.  [Create a new definition from a scratch](#1-create-a-new-definition) 
2.  [Upload a definition from JSON format](#2-upload-a-definition-from-json-format)
3.  Clone an existing definition (more in [Actions](#actions) section)

### 1. Create a new definition
To create a new training definition click on the top right button ![Create-button](../../img/buttons/create-button.png). This will open training definition editor page.

#### Create Training Definition panel
In the first panel of the training definition editor, the designer can edit fields that describe the new definition. When the designer is done they can either click on:
1.  ![Create-button](../../img/buttons/create-button.png) that will create the new definition and redirect them back to Training Definition Overview
2.  ![Create-and-continue](../../img/buttons/create-and-continue-button.png) that will allow the designer to edit **authors** and **levels** of the definition.

<p align="center">
    <img src="../../../img/kypo-portal/trainings/training-definition/TD-create-panel.png">
</p>

#### Edit Authors panel
In the second panel of training definition editor the designer can add and remove authors from this definition: 

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-edit-authors.png">
</p>

#### Edit Levels panel
In the third panel the designer can add, delete, and edit game levels of the training definition:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-edit-levels.png">
</p>

To add a new level the designer can click ![Add-button](../../img/buttons/add-button.png) that will roll down a menu in which the designer can choose a type of the new level:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-levels.png">
</p>

##### I. Game level
At the game level, a player can access a virtual network inside the sandbox to find a solution to the problem assigned by level content. The designer can fill this form to specify details of the new level (when the designer is done editing level they must save changes with ![save](../../img/buttons/save-button.png) button):

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-GL-panel.png">
</p>

Under the game level editing form there is a forth additional panel that the designer can use to create, delete and edit **hints** that are associated with a given game level:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-hint-panel.png">
</p>

A new hint can be added with the ![add-button](../../img/buttons/add-button.png) button and edited with the following form (when the designers finish the editing of hints they must save changes with ![save](../../img/buttons/save-button.png) button):

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-hint-edit.png">
</p>

##### II. Assessment level
In the assessment level, the players answer a list of questions. Content of this level can be edited with the following form (when the designers finish the editing of this level they must save changes with ![save](../../img/buttons/save-button.png) button):

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-AL-panel.png">
</p>

Under the assessment level editing form there is an additional **Questions** panel to create, delete and edit questions associated with given assessment level:   
 
<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-questions-panel.png">
</p>

A designer can choose to create a test or questionnaire, so the creation of the question may differ based on the type of assessment. A new question can be added with the ![add-button](../../img/buttons/add-button.png) button that will roll down menu where the designer can choose a type of the new question:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-question.png">
</p>

Each type has its specific editing form (when the designers finish the questions they must save changes with ![save](../../img/buttons/save-button.png) button) button):

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-questions-edit.png">
</p>

##### III. Info Level
In info level the player can only read content specified by the designer in the following form:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-IL-panel.png">
</p>


### 2. Upload a definition from JSON format
To upload a training definition the designer can click in the **Training Definition Overview** on the top right ![upload-button](../../img/buttons/upload-button.png) button. This will open the following window:

<p align="center">
  <img src="../../../img/kypo-portal/trainings/training-definition/TD-upload-panel.png">
</p>


The designer can upload training definitions that were stored in the JSON file. This use-case is useful in the situation when the designer wants to re-use the training definition stored in the past.