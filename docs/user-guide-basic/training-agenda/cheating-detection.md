This page details the use of cheating detection methods and interpretation of detected results on linear training instance. Detection methods can be easily and freely used on any training instance of linear training definition, however, to fully understand the relevancy and applicability of each detection method, read the whole documentation.

## Cheating Detection Overview
To access the main page for cheating detections on a training instance click the ![Cheating detection button](/img/buttons/cheating-detection-button.png){: .inline-button } button in training instance overview.

![cheating-detection-overview](img/user-guide-basic/training-agenda/cheating-detection/cheating-detection-overview.png)

This page lists all previously executed cheating detections by all organizers on the given training instance. From here you can access pages for creating new cheating detections and viewing detected results. Cheating detections provide additional information in the table:

1. Execution time and name of executor
2. The state of the detection (Finished/Running)
3. Number of detected results
4. The state of detection methods (Disabled/Running/Finished)
5. Actions that can be executed on a cheating detection

Each cheating detection has these actions that can be executed:

??? hhhh "Show Results"

    Click the button to move to the page containing suspicious events that were found.

??? download "Export"

    Click the button to download an archive containing all detected events and their information.

??? pencil "Rerun"

    Click the button, and the cheating detection with its specified methods will be forced to run again from scratch. Once a cheating detection for a training is created, this is the preferred method of executing the cheating detection again after a period of time. This way you won't have to go through the creation process again.

??? trash-can "Delete"

    Click the button and cheating detection with all its detected events and data will be deleted.

## Create Cheating Detection

![cheating-detection-create](/img/user-guide-basic/training-agenda/cheating-detection/cheating-detection-create.png){: .shadow .center .radius-image }

In this page you can create a new cheating detection with specified detection methods. Each of these methods executes an algorithm to detect suspicious activities on logs and data, that was provided by the trainees up to this point in time. Cheating detections can be executed both while the training is still running and after the training was finished. You can execute multiple cheating detections with different methods and parameters, however, it is not advised to execute them at the same time in trainings with a lot of participants (100+) as it may negatively affect performance.

It is worth noting, that these detection methods do not irrefutably incriminate trainees of cheating. Some of the detection methods can also supplement each other, so it's worth using all the detection methods, when they are sensible in the context.

So far the cheating detection supports these methods:

??? pencil "Answer Similarity"

    Occurs when a trainee submits an answer for a level that was incorrect, but was a correct answer for another trainee (who most likely shared his answer).
    This detection method is relevant for APG trainings, where answers for trainees are randomly generated.

??? pencil "Location Similarity"

    Occurs when two or more trainees submit the answer to a level from the same domain. This detection is relevant for trainings where all participants are expected to have different domains (excludes trainings where all trainees are connected to CyberRangeCZ Platform from the same IP network).

??? pencil "Time Proximity"

    Occurs when two or more trainees submit a correct answer for a level in a short time window. This time window can be specified in a label 'proximity threshold' in seconds, with default value being two minutes. This detection is relevant for trainings that span a longer time period (for example two weeks), but is irrelevant for a short term training (one hour exam).

??? pencil "Minimal Solve Time"

    Occurs when a trainee solves a level in a shorter time that is the specified minimal possible solve time for the level. For this detection to be relevant, minimal solving time must be reasonably specified when creating a level in training definition. Too much time will result in many false negatives while too little time in false positives. This detection might not prove someone cheated right away, but can be a great supplement for all the detection methods described above.

??? pencil "No Commands"

    Occurs when a trainee solves a level without using any commands in a provided console, when the level specifically required it. The requirement for using commands is specified in the box 'are_commands_required' when creating a level in training definition.

??? pencil "Forbidden Commands"

    Occures when a trainee submits a command that was specified as 'forbidden' by the instructor. When ticking this checkbox, the instructor gets access to a new panel where he can setup which commands he wants to forbid. Each forbidden command consists of the command string and command console type. The console type can be either BASH or Metasploit.

## Detection Events of Cheating Detection

![detection-events-overview](/img/user-guide-basic/training-agenda/cheating-detection/detection-events-overview.png){: .shadow .center .radius-image }

This page lists a table of detected cheating events with basic information about the events. For more specific information, the instructor can click in the action *show details* to move to detection event detail page.

The basic information includes:

1. Title of the level and its id
2. Number of players who participated in the suspicious event
3. When it was detected
4. Type of the event
5. Actions

You can access detailed information for a specific event by clicking on the *show detailed information* action button.

### Detection Event Detail

![detection-events-detail](/img/user-guide-basic/training-agenda/cheating-detection/detection-events-detail.png){: .shadow .center .radius-image }

This page provides detailed information for a detection event and its participants based on the event type. Most of the information is similar for each type of detection. Below is a list of information that are specific and relevant for each detection event type.

#### Detection Event of type 'Answer Similarity'

**Answer** - The answer that was used by participants.
**Answer owner** - Player that potentially shared his answer with other participants.

#### Detection Event of type 'Location Similarity'

**Domain name** - name of the domain service that was shared by all participants of the event.
**Is address of deployment** - Boolean value that specifies if the domain is the same as the domain name where CyberRangeCZ Platform is deployed.

#### Detection Event of type 'Time Proximity'

**Proximity threshold** - specified time window (in seconds), in which two submissions from distinct players on the same level are flagged.

#### Detection Event of type 'Minimal Solve Time'

**Minimal solve time** - minimum time to solve level (specified in training definition).
**Solved in time** - time it took for the player to solve the level.

#### Detection Event of type 'No Commands'

No specific information added.

#### Detection Event of type 'Forbidden Commands'

**List of forbidden commands** - list of forbidden commands
**Command timeline** - a timeline of commands that were submitted by the trainee in the training
