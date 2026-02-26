## Sandboxes Creation
1. A sandbox definition is created by instructors according to this [format](../../user-guide-advanced/sandboxes/sandbox-definition.md) and stored as a Git repository.
2. In the CyberRangeCZ Platform Portal, a record about the sandbox definition is created via the [Sandbox Definition Overview](../../user-guide-basic/sandbox-agenda/sandbox-definition.md) page by entering the URI to the respective Git repository from the previous step.
3. From the sandbox definition created in the CyberRangeCZ Platform Portal, a pool with a specified size can be created by following these [steps](../../user-guide-basic/sandbox-agenda/pool.md#create-pool).
4. Sandboxes in the cloud are allocated by clicking the allocation button of the respective pool. Two actions are automatically performed:
    1. The respective sandbox definition is downloaded from the Git repository, parsed, and processed.
    2. Sandboxes are created in the cloud according to the sandbox definition.
5. Sandboxes can be used in two ways:
    1. An instructor can access VMs inside sandboxes using SSH or GUI and perform any actions. See [Sandbox SSH Acccess](../../user-guide-advanced/sandboxes/sandbox-access.md#sandbox-access).
    2. Sandboxes are used as part of the trainings. See the [Training Creation](#training-creation) workflow.


![Sandboxes workflow diagram](/img/basic-concepts/workflow-sanboxes-cloud.svg){: .center style="max-width: 420px;" }

## Training Creation

### Before Training
1. Training definition can be created via the [Create Linear Training Definition](../../user-guide-basic/training-agenda/training-definition/linear-training-definition.md#add-a-new-definition) or the [Create Adaptive Training Definition](../../user-guide-basic/training-agenda/training-definition/adaptive-training-definition.md#add-a-new-definition) page independently on the sandbox definition.
2. Training instance can be created via the [Create/Edit Training Instance](../../user-guide-basic/training-agenda/training-instance.md#createedit-training-instance) page specifically for the selected available training definition. Option [local environment](../terminology.md#training) must be disabled.
3. An unlocked pool of sandboxes **created for the training** is assigned to the training instance in the second panel [Assign Pool](../../user-guide-basic/training-agenda/training-instance.md#assign-pool) when editing the training instance.
4. Each training instance has a partially generated access token which the instructor hand over to trainees so they can access [linear](../../user-guide-basic/training-agenda/training-run/linear-training-run.md#training-run) or [adaptive](../../user-guide-basic/training-agenda/training-run/adaptive-training-run.md#training-run) training runs.


### During Training
5. Trainees [access Training Run](../../user-guide-basic/training-agenda/training-run/linear-training-run.md#1-access-training) using the obtained access token. Trainees can resume their accessed training runs if the training instance is still active.
6. Each training run has assigned a specific sandbox and trainees can access VMs in this sandbox using [Terminal Remote Access](../../user-guide-advanced/sandboxes/sandbox-access.md#terminal-remote-access) (SSH) or [Web-based Access](../../user-guide-advanced/sandboxes/sandbox-access.md#web-based-access) (Apache Guacamole, Spice).
7. An organizer of training instance can watch the real-time progress of trainees and can see their [linear training run results](../../user-guide-basic/training-agenda/visualizations/visualizations-for-linear.md#progress-of-training-instance) during the training.

!!! note
    Results for the adaptive training runs will be added in near future.

### After Training
8. When the training instance is finished, the [results](../../user-guide-basic/training-agenda/visualizations/visualizations-for-linear.md#results-of-training-instance) are available and ready for further evaluation.
9. The assigned pool is unassigned from the training instance and deleted using the delete button on [Pool Overview](../../user-guide-basic/sandbox-agenda/pool.md#pool-overview) page to free resources in the cloud. The respective training instance can be deleted using delete button on [Training Instances Overview](../../user-guide-basic/training-agenda/training-instance.md#training-instance-overview) page.

![Trainings workflow diagram](/img/basic-concepts/workflow-trainings-cloud.svg){: .center style="max-width: 420px;" }



