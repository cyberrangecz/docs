# Visualizations for Linear Training

The following visualizations relate to the linear form of the training. The sections [For Instructors](#for-instructors) and [For Trainees](#for-trainees), respectively, describe the purpose and means of manipulation with the visualizations.

## For Instructors

### Progress of Training Instance 

As an instructor, you can see the ongoing course of the training runs and further filter information on demand in the tab **Progress**. The interface consists of several sections for interaction with the visualization. Each section (**A** to **D**, see the figure below) is further described in detail.

<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TI-progress.png">
</p>

!!! info
    In the visualization, exclamation marks (![exclamation_mark](../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/exclamation.png)) can appear next to trainees or level tiles. They indicate a situation that may need further attention - upon a mouse over, textual information appears. On a mouse click on the mark, it fades to signalize that the issue is being solved and does need to be highlighted.

**A - Overview Timeline**

 The time displayed in the upper right corner indicates the estimated end of the session based on the current progression. A small arrow ![arrow](../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/arrow.png) denotes the original scheduled end time to show the deviation from the schedule. On hover, exact scheduled end time shows. As the training session progresses, the timeline fills accordingly.

**B - Trainee Selection**

All trainees (their avatars and/or names) are listed here. Each trainee can be selected or deselected upon mouse click, to show/hide their training progression in the visualization below. On mouse hover on a visible trainee, their run  in the visualization highlights. 

[//]: <> (Above the grid is a text summary with the number of all trainees and the number of those currently displayed in the visualization. On click on the corresponding text on the right, all trainees show or hide accordingly.)

**C - Level Selection**

These tiles represent individual training levels. Each level tile also holds information regarding the number of trainees who currently solve the level. On hover, level name and correct flag shows in a tooltip. Additionally, the last tile displays all the trainees who have already finished the whole training session. For each level, you can display it’s trainees on click.

**D - Progress Visualization**

It gives a full picture of the trainees walkthrough. Upon filtering in the preceding sections, selected trainees are displayed here. 

Each row represents an individual trainee. Bars of each row are training levels - gray levels are finished levels, current levels are colored green/yellow/red, according to their delay opposed to the scheduled amount of time. The stripped bars denote the scheduled time for the ongoing or upcoming levels.

The bars can display events of the trainees. When taking a hint ![hint](../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/hint.png) or submitting a wrong flag ![wrong-flag](../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/flag.png), the event displays in the visualization, colored the same as its level. Multiple events of the same type triggered in quick succession show as one, with a corresponding number on it. On mouse-over, detailed information tooltip shows.

**Individual Trainee Detail**

More detailed individual trainee progress can be displayed. Upon click on a trainee avatar or name on the left side of the training runs visualization, a new window shows:

<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/progress-detail.png">
</p>

Here, the additional line chart shows the activity of the trainee for the ongoing level.

### Results of Training Instance 

The page displays all collected data about the training instance divided into five tabs. The overview tab displays all graphs and tables in a single tab. Tabs [Score Development](#score-development), [Score Scatter Plot](#score-scatter-plot), and [Progress](#progress) provides various views on trainees activity in the training.

#### Score Development 

The tab displays a graph with a time development of the trainees' scores marked in the table under the graph. The graph also displays various types of events (displayed by a small circle). To visualize events taken by trainees, check/uncheck a checkbox displayed next to the table with participants. To zoom in or out, hold Ctrl + Scroll while scrolling with the mouse wheel.

<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TI-score-dev.jpg">
</p>

#### Score Scatter Plot 

This visualization provides an overview of the training results. It helps to compare the score and duration of the whole training or individual levels. Dots show the positions of the trainees based on score and time. They indicate the correlation between the two factors and help to pinpoint the outliers or allocate clusters.


<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TI-score-scatter.png">
</p>

#### Final Training Runs View

This visualization is a view on available data distilled from the "Progress of Training Instance". It supports additional interaction (such as level sorting by their duration) and gives a full picture of the trainee walkthrough. The color scale helps to highlight individual levels for all trainees as well as their usage of hints or submission of wrong flags for the levels. It helps to find skilled trainees or flaws in the training design by observing the details of its progression.

<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TI-score-progress.jpg">
</p>


#### Assessment
Displays statistics of individual assessment answers.
 
<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TI-assessment.png">
</p>

## For trainees

After a trainee finishes a training run, a set of visualizations of their behavior displays. Since the trainees should decode all information easily without any further guidance, the interface is designed to be simple and straightforward.

<p align="center">
  <img src="../../../../../img/user-guide-basic/training-agenda/visualizations/linear-training-visualizations/TR-results.jpg">
</p>
