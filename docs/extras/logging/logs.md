In the KYPO CRP, we monitor the trainees' progress during training by logging the various events. Currently, we differentiate between two major types of logs:

 * **Training events**:  Any action performed by the trainee on the KYPO portal web page is considered to be a Training event (e.g., taking a hint, solving a level, finishing a run, ...). These events are mainly used for real-time visualization of the Training run. Based on training events, organizers can offer individual help to struggling trainees or, on the other hand, take notice of excellent students.
 * **Commands**: All commands executed by the students inside the sandbox command line are logged. These logged commands offer detailed information about all students' actions while completing the assignment. The organizers can then use command logs to evaluate each student's actions, and the complexity of the solutions students came up with during the Training run.
 

## Training Events - Linear 

### Common Fields
 
* **sandbox_id**: the ID of a sandbox instance
* **pool_id**: the ID of a pool
* **training_definition_id**: the ID of a training definition
* **training_instance_id**: the ID of a training instance
* **training_run_id**: the ID of a training run 
* **training_time**: the time that has elapsed since the start of a training run
* **total_training_score**: total score achieved in training levels
* **total_assessment_score**: total score achieved in assessment levels
* **actual_score_in_level**: actual score in a current level
* **level**: the ID of a level
* **level_order**: order of a level in a training definition
* **user_ref_id**: ID of the user
* **timestamp**: time at which the event occurred
* **type**: type of the event (*AssessmentAnswers, CorrectAnswerSubmitted, HintTaken, LevelCompleted, LevelStarted, SolutionDisplayed, TrainingRunEnded, TrainingRunResumed, TrainingRunStarted, TrainingRunSurrendered, WrongAnswerSubmitted*)

### Additional fields

Each type of event might have additional fields. 

* AssessmentAnswers 
    * **answers**: all answers submitted by the trainee in the JSON format
* CorrectAnswerSubmitted
    * **answers_content**: answer submitted by the trainee
* HintTaken
    * **hint_id**: the ID of a hint
    * **hint_penalty_points**: points that are lost when a hint is taken
    * **hint_title**: title of a hint
* LevelCompleted
    * **level_type**: type of a level (INFO, ASSESSMENT, TRAINING)
* LevelStarted
    * **level_type**: type of a level (INFO, ASSESSMENT, TRAINING)
    * **max_score**: maximal score that can be achieved for a level
    * **level_title**: title of a level
* SolutionDisplayed
    * **penalty_points**: 
* TrainingRunEnded
    * **start_time**: training run start time
    * **end_time**: training run end time
* WrongAnswerSubmitted
    * **answer_content**: content of a wrong submitted answer
    * **count**: number of wrong tries (indicates the sequence number of the wrong answer) in a current level

### Example

**Common Fields**

```
{
   "sandbox_id": 10,
   "pool_id": 3,
   "training_definition_id": 1, 
   "training_instance_id": 1,
   "training_run_id": 1,
   "training_time": 0,
   "total_training_level_score": 0,
   "total_assessment_level_score": 0,
   "actual_score_in_level": 0,
   "level": 1,
   "level_order": 0,
   "user_ref_id": 1,
   "timestamp": 1636706806953
   "type": "cz.muni.csirt.kypo.events.trainings.TrainingRunStarted"
}
```

**Additional Fields**

```
{
   ### AssessmentAnswers
   "answers": "[{ \"questionId\": 4, \"answers\": [\"Graphical user interface of KYPO\"] }, { \"questionId\": 5, \"answers\": [{ \"statementOrder\": 1, \"optionOrder\": 1 }, { \"statementOrder\": 2, \"optionOrder\": 1 }, { \"statementOrder\": 0, \"optionOrder\": 0 }] }, { \"questionId\": 6, \"answers\": [\"null\"] }]"

   ### CorrectAnswerSubmitted
   "answer_content": "Top_Secret_Flag"

   ### HintTaken
   "hint_id": 15,
   "hint_penalty_points": 5,
   "hint_title": "Tool for password attacks"

   ### LevelCompleted
   "level_type": "ASSESSMENT"

   ### LevelStarted
   "level_type": "TRAINING",
   "max_score": 50,
   "level_title": "Finding open ports"

   ### SolutionDisplayed
   "penalty_points": 10

   ### TrainingRunEnded
   "start_time": 1636706806877,
   "end_time": 1636706947806

   ### WrongAnswerSubmitted
   "answer_content": "Very_Bad_Flag",
   "count": 3
}

```



## Training Events - Adaptive 

### Common Fields

* **sandbox_id**: the ID of a sandbox instance
* **pool_id**: the ID of a pool
* **training_definition_id**: the ID of a training definition
* **training_instance_id**: the ID of a training instance
* **training_run_id**: the ID of a training run 
* **training_time**: the time that has elapsed since the start of a training run
* **phase_id**: the ID of a phase
* **phase_order**: order of a phase in a training definition
* **task_id**: the ID of a task 
* **task_order**: order of a task in a phase 
* **user_ref_id**: the ID of a user
* **timestamp**: time at which the event occured
* **type**: type of the event (*CorrectAnswerSubmitted, PhaseCompleted, PhaseStarted, QuestionnaireAnswers, SolutionDisplayed, TrainingRunEnded, TrainingRunResumed, TrainingRunStarted, TrainingRunSurrendered, WrongAnswerSubmitted*)



### Additional fields

Each type of event might have additional fields. 

* CorrectAnswerSubmitted
    * **answers_content**: answer submitted by a trainee
* PhaseCompleted
    * **phase_type**: type of a phase (INFO, QUESTIONNAIRE, TRAINING)
    * **phase_title**: title of a phase
* PhaseStarted
    * **phase_type**: type of a phase (INFO, QUESTIONNAIRE, TRAINING)
    * **phase_title**: title of a phase
* QuestionnaireAnswers 
    * **answers**: all answers submitted by a trainee in the JSON format
* TrainingRunEnded
    * **start_time**: training run start time
    * **end_time**: training run end time
* WrongAnswerSubmitted
    * **answer_content**: content of the wrong submitted answer
    * **count**: number of wrong tries (indicates the sequence number of the wrong answer) in the current phase

### Example

**Common Fields**
```
{
   "sandbox_id": 11,
   "pool_id": 3,
   "training_definition_id": 52,
   "training_instance_id": 152,
   "training_run_id": 5,
   "training_time": 2516,
   "phase_id": 6, 
   "phase_order": 1,
   "task_id": null, 
   "task_order": null,
   "user_ref_id": 1,
   "timestamp": 1636712942803,
   "type": "cz.muni.csirt.kypo.events.adaptive.trainings.PhaseStarted"
}
```

**Additional Fields**
```
{
   ### CorrectAnswerSubmitted
   "answer_content": "Top_Secret_Flag"

   ### PhaseCompleted
   "phase_type": "QUESTIONNAIRE",
   "phase_title": "Finding open ports"

   ### PhaseStarted
   "phase_type": "TRAINING",
   "phase_title": "Finding open ports"

   ### QuestionnaireAnswers
   "answers":"[QuestionAnswer{questionAnswerId=1, answers='[None]'}, QuestionAnswer{questionAnswerId=2, answers='[None]'}, QuestionAnswer{questionAnswerId=3, answers='[None]'}, QuestionAnswer{questionAnswerId=4, answers='[None]'}, QuestionAnswer{questionAnswerId=5, answers='[None]'}, QuestionAnswer{questionAnswerId=6, answers='[None]'}, QuestionAnswer{questionAnswerId=7, answers='[Low]'}, QuestionAnswer{questionAnswerId=8, answers='[Medium]'}]"

   ### TrainingRunEnded
   "start_time": 1636706806877,
   "end_time": 1636706947806

   ### WrongAnswerSubmitted
   "answer_content": "Very_Bad_Flag",
   "count": 3
}
```


## Commands 

### Fields

* **cmd**: executed command
* **cmd_type**: type of command *(bash-command, msf-command)*
* **wd**: current working directory
* **username**: name of the currently logged in user logged into the machine who executed the command
* **timestamp_str**: time at which the command has been executed
* **hostname**: unique name of the machine in a sandbox
* **ip**: internal IP address of the machine in a sandbox 
* **sandbox_id**: the ID of a sandbox instance
* **pool_id**: the ID of a pool


### Example 

```
{
   "cmd": "msfconsole",
   "cmd_type": "bash-command",
   "wd": "/home/debian",
   "username": "debian",
   "timestamp_str": "2021-11-12T10:29:37.988Z",
   "hostname": "home",
   "ip": "10.10.30.5",
   "sandbox_id": "11",
   "pool_id": "3"
}
```

The example logs from the past training events can be found at: [https://gitlab.ics.muni.cz/muni-kypo-trainings/datasets](https://gitlab.ics.muni.cz/muni-kypo-trainings/datasets).
