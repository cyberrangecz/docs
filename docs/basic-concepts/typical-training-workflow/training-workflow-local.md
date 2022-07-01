## Sandboxes Creation
1. A sandbox definition is [created using Cyber Sandbox Creator](https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator/-/wikis/3.0/Generating-a-Sandbox) and stored in a Git repository (see [6. Configure access to the Gitlab repository](../../installation-guide/kypo-crp-deployment/#configure)). 
2. In the KYPO Portal, a record about the sandbox definition is created via the [Sandbox Definition Overview](../../user-guide-basic/sandbox-agenda/sandbox-definition/) page by entering the URI to the respective Git repository from the previous step.
3. An instructor can see and check the topology of the sandbox definition via KYPO Portal. 

<p align="center" >
      <img style="width: 90%" src="../../../img/basic-concepts/KYPO-workflow-sandboxes-local.png">
</p>


## Training Creation

### Before Training 
1. Training definition can be created via the [Create Linear Training Definition](../../../user-guide-basic/training-agenda/training-definition/linear-training-definition/#add-a-new-definition) or the [Create Adaptive Training Definition](../../../user-guide-basic/training-agenda/training-definition/adaptive-training-definition/#add-a-new-definition) page independently on the sandbox definition.
2. Training instance can be created via the [Create/Edit Training Instance](../../../user-guide-basic/training-agenda/training-instance/#createedit-training-instance) page specifically for the selected training definition. Option [local environment](../../terminology/#training) must be enabled. 
3. A sandbox definition **created for the training** is assigned to the training instance in the second panel [Assign Sandbox Definition](../../../user-guide-basic/training-agenda/training-instance/#assign-sandbox-definition) when editing the training instance.
4. Each training instance has a partially generated access token which the instructor hand over to trainees so they can access [linear](../../user-guide-basic/training-agenda/training-run/linear-training-run/#training-run) or [adaptive](../../user-guide-basic/training-agenda/training-run/adaptive-training-run/#training-run) training runs. 


### During Training
5. Trainees [access Training Run](../../../user-guide-basic/training-agenda/training-run/linear-training-run/#1-access-training) using the obtained access token. Trainees can resume their accessed training runs if the training instance is still active.
6. Each training run should have a defined special access level/phase which should contain a URL to the Git repository of sandbox definition and instructions on how to build a sandbox locally.
7. Users run the command provided in the access level/phase to run the local sandbox and wait until it is successfully built and ready, see the [documentation of Cyber Sandbox Creator](https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator/-/wikis/3.0/Building-and-Using-a-Sandbox).
8. Users can access machines within the local sandbox using the console or SSH access.
9. An organizer of training instance can watch the real-time progress of trainees and can see their [linear training run results](../../../user-guide-basic/training-agenda/visualizations/visualizations-for-linear/#progress-of-training-instance) during the training. 

!!! note
    Results for the adaptive training runs will be added in near future.

### After Training
10. When the training instance is finished, the [results](../../../user-guide-basic/training-agenda/visualizations/visualizations-for-linear/#results-of-training-instance) are available and ready for further evaluation.

![KYPO-workflow-trainings](../../img/basic-concepts/KYPO-workflow-trainings-local.png)



