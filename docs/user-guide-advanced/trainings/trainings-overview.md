The CyberRangeCZ Platform is also used to create cybersecurity exercises and trainings. When working with the trainings, it is required to familiarize yourself with the following terms [Training Definition](#training-definition), [Training Instance](#training-instance), and [Training Run](#training-run).

## Training Definition

The content of the whole exercise is described using so-called training definitions. The platform supports **linear** training definitions, which also support the technique of the [Automatic Problem Generation (APG)](#automatic-generation-problem-apg-in-linear-training-definition). A training definition includes information about the title, notes for instructors, and learning outcomes, and further consists of multiple **[levels](#levels)**. A created training definition can be download as a file in JSON format. It is a good practice to store Training Definition in the Git repository next or close to the repository of Sandbox Definition that is specially created for that Training Definition.

!!! note
    Creating APG Training Definition requires field Generate variant sandboxes to be selected while [creating training definition](../../user-guide-basic/training-agenda/training-definition/linear-training-definition.md#create-linear-training-definition-panel).

### Linear

#### Levels
 The *linear definition* consist of three types of levels:

1. **Info Level**: Contains information for the trainee (welcome message or important information about the following levels).
2. **Training Level**: The user has to solve a predefined assignment in the level. By solving the assignment, the trainee acquires a secret answer, and after submitting the answer, they can continue to the next level of the training.
3. **Assessment Level**: It can be either a test or a questionnaire, and it serves to test users’ knowledge or get feedback from users. The assessment can contain one of the following types of questions:
    * **Multiple choice question (MCQ)**: Trainees are asked to select one or multiple answers from the choices offered as a list.
    * **Extended matching item (EMI)**: Trainees are asked to pair items from row and column that are semantically related.
    * **Freeform question (FFQ)**: Trainees are asked to type the answer to the submit field.
4. **Access Level**: Contains information on how to access either local or cloud sandbox.

#### Automatic Generation Problem (APG) in Linear Training Definition
**Automatic Problem Generation** is a technique of defining various problem instances. In CyberRangeCZ Platform, it is achieved by using variant answers for each [Training Run](#training-run) that can reduce the threat of copied or leaked answers. APG training definition requires specific [Sandbox Definition](../../user-guide-advanced/sandboxes/sandbox-definition.md) with **variables.yml** file. The file specifies variables whose values are automatically generated for each sandbox instance. The generated values then can be used during provisioning to set secret answers inside the sandbox (e.g., filename, port, username, etc.). Behind the scenes, generated values are stored to the special **answers storage**.

When creating a training level, a designer can specify either:

* **Correct Answer - Static** *(uncheck Variant Answers)*: All trainees' answers are the same.
* **Correct Answer - Variable Name** *(check Variant Answers)*: Answers are unique for each sandbox and therefore for each trainee. A variable name set to this field must be identical to a variable from **variables.yml**. Therefore, the exact values of the variables don't have to be generated at the creation time of the training definition. The trainee's submitted answer is then compared to a value from the **answers storage**.


!!! note
    Training definition is considered APG if it has at least one training level with field **Correct Answer - Variable Name** set.

!!! note
    Adaptive training definitions (composed of phases and driven by the Smart Assistant) have been decommissioned and are no longer part of the CyberRangeCZ Platform.

## Training Instance

A time-limited instance of a training definition during which trainees have access to training. The whole training instance progress is managed by instructors who can monitor events made by trainees that are displayed in various graphs and tables that may differ based on the type of assigned training definition. Each training instance has an assigned [pool](../../user-guide-advanced/sandboxes/sandboxes-overview.md#pool) with sandboxes.

## Training Run

The training run represents a single run of the training of the particular trainee. The run is accessed based on the access token obtained from the training instance instructor. The trainee enters the access token to the particular field. If the token is valid, the training run starts (behind the scenes, a sandbox is assigned to that training run from the pool associated with the particular training instance).

## Graphical Representation

### Overall
The following chart displays interconnection between trainings and [sandboxes](../sandboxes/sandboxes-overview.md).

![Training-Sandbox relations](/img/user-guide-advanced/trainings/basic-elements.svg){: .center style="max-height: 600px;"}
