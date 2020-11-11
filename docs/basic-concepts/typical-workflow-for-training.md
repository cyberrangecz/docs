Before starting a training run, several steps must be performed. These steps are not necessarily performed by a single user and they are usually divided among several users with a role [instructor](../../user-guide-advanced/users-and-groups/roles/). The whole workflow of creating training is divided into two parts, as it also includes the creation of the sandboxes.

1. **[Sandboxes Creation](#sandboxes-creation)**
2. **[Training Creation](#training-creation)**

## Prerequisites
It is assumed that KYPO CRP is installed according to the [installation guide](../../installation-guide/installation-guide-overview/) and created KYPO CRP instance is connected to the OpenStack cloud service and through the respective microservice, it can create and manage sandboxes inside the cloud via available APIs.


## Sandboxes Creation
1. A sandbox definition is created by instructors according to this [format](../../user-guide-advanced/sandboxes/sandbox-definition/) and stored as a Git repository (see [7. Configure access to the Gitlab repository](../../installation-guide/kypo-crp-deployment/#configure)). 
2. In the KYPO Portal, a record about the sandbox definition is created via the [Sandbox Definition Overview](../../user-guide-basic/sandbox-agenda/sandbox-definition/) page by entering the URI to the respective Git repository from the previous step.
3. From the sandbox definition created in the KYPO Portal, a pool with a specified size can be created by following these [steps](../../user-guide-basic/sandbox-agenda/pool/#create-pool). 
4. Sandboxes in the cloud are allocated by clicking the allocation button of the respective pool. Two actions are automatically performed:
    1. The respective sandbox definition is downloaded from the Git repository, parsed, and processed. 
    2. Sandboxes are created in the cloud according to the sandbox definition. 
5. Sandboxes can be used in two ways:
    1. An instructor can access VMs inside sandboxes using SSH and perform any actions. See [Sandbox SSH Acccess](../../user-guide-advanced/sandboxes/sandbox-ssh-access/).
    2. Sandboxes are used as part of the trainings. See the [Training Creation](#training-creation) workflow.
  

<p align="center" >
      <img style="width: 90%" src="../../img/basic-concepts/KYPO-workflow-sandboxes.png">
</p>


## Training Creation

### Before Training 
1. Training definition can be created via the [Create Training Definition](../../user-guide-basic/training-agenda/training-definition/#add-a-new-definition) page independently on the sandbox definition.
2. Training instance can be created via the [Create/Edit Training Instance](../../user-guide-basic/training-agenda/training-instance/#createedit-training-instance) page specifically for the selected available training definition.
3. An unlocked pool of sandboxes **created for the training** is assigned to the training instance in the second panel [Assign Pool](../../user-guide-basic/training-agenda/training-instance/#2-assign-pool) when editing the training instance.
4. Each training instance has partially a generated access token which the instructor hand over to trainees so they can access [training runs](../../user-guide-basic/training-agenda/training-run/#training-run). 


### During Training
5. Trainees [access Training Run](../../user-guide-basic/training-agenda/training-run/#1-access-training) using the obtained access token. Trainees can resume their accessed training runs if the training instance is still active.
6. Each training run has assigned a specific sandbox and trainees can access VMs in this sandbox using [Sandbox SSH Access](../../user-guide-advanced/sandboxes/sandbox-ssh-access/) or a [Spice console](../../user-guide-basic/training-agenda/training-run/#vm-manipulation).
7. An organizer of training instance can watch real-time progress of trainees and can see their [training run results](../../user-guide-basic/training-agenda/training-run/#training-run-results) during the game. 

### After Training
8. When the training instance is finished, the [results](../../user-guide-basic/training-agenda/training-instance/#results-of-training-instance) are available and ready to be downloaded for further evaluation.
9. The assigned pool is unassigned from the training instance and deleted using the delete button on [Pool Overview](../../user-guide-basic/sandbox-agenda/pool/#pool-overview) page to free resources in the cloud. The respective training instance can be deleted using delete button on [Training Instances Overview](../../user-guide-basic/training-agenda/training-instance/#training-instance-overview) page.

![KYPO-workflow-trainings](../img/basic-concepts/KYPO-workflow-trainings.png)



