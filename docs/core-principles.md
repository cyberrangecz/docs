KYPO is a unique project that serves as a training center for cybersecurity, which deals with research, development, and creation of an environment for the pre-analysis of attacks on critical information infrastructures. In this environment, it is possible to implement comprehensive security training and exercises. The result of the project is a KYPO platform used to simulate computer infrastructures in a controlled cloud environment to achieve high flexibility, scalability, isolation, and portability. The platform allows you to create fully-functional virtual networks with a full-fledged operating system and network devices that faithfully emulate real-world systems. In the environment, cybersecurity attacks can be tested repeatedly without any impact on the real infrastructure. It thus provides the opportunity to create and try out various cybersecurity scenarios reminiscent of real-world situations that take place independently of the Internet connection.


## Use cases
KYPO focuses on three use cases:

  1. **Education and Training**: Verifying and acquiring individuals' knowledge through learning activities such as training, Capture the flag (CTF) games or school subjects. KYPO provides the ability to create computer security scenarios that can be simulated on different types of operating systems in the same environment through virtualization. 
  2. **Cyber Research and Development**: Developing, testing, and demonstrating new methods for detecting and mitigating network attacks on critical infrastructure. In this case, KYPO provides an empty virtual environment with the possibility of monitoring infrastructure. Users can create various computer networks and monitor their network traffic. Statistics from this data are subsequently stored and analyzed within the KYPO infrastructure.
  3. **Digital Forensic Analysis**: It partly builds on the previous use case and covers basic forensic analysis, which is partially automated. An image with a malicious machine is placed in the virtual environment, the activities of which are then monitored using a set of automatic and dynamic analyzes. Thanks to the virtual environment, it is possible to dynamically change the environment according to the activities of the machine and monitor its behavior.


## Terminology
Before starting with the KYPO platform, you should familiarize yourself with the basic terminology that is used in it. As mentioned before, the KYPO platform is primarily used to provide virtual environment and create cybersecurity exercises and trainings. For trainings there is also need to have a virtual environment and description of their content.

### Trainings 
In the KYPO environment, the following terminology is associated with the trainings: 

* **Training Definition**: The progress of the whole exercise must be somehow described. For this purpose, users called **training designers** create *training definitions*. Training definition includes information about the title, notes for instructors, learning outcomes, and levels that consist of. There are three types of levels: 
    1. <ins>***Info Level***</ins>: Contains information for the player (welcome message or important information about the following levels).
    2. <ins>***Game Level***</ins>: In the level, the user has to solve a predefined assignment. By solving the assignment, the player acquires a secret flag, and after submitting the flag, they can continue to the next level of the training. 
    3. <ins>***Assessment Level***</ins>: Can be either a test or a questionnaire, and it serves to test users’ knowledge or gets feedback from users. The assessment can contain one of the following types of question: 
        * *MCQ (Multiple choice question)*: Players are asked to select one or multiple answers from the choices offered as a list.
        * *EMI (Extended matching items)*: Players are asked to pair items from row and column that are semantically related. 
        * *FFQ (Freeform question)*: Players are asked to type the answer to the submit field.

* **Training Instance**: A time-limited period in which players can participate in training which is specified by the assigned training definition. The whole progress of training instance is managed by **training organizers (instructors)** who can monitor events made by players that are displayed in various graphs and tables. Each training instance has an assigned *pool*. 

* **Training Run**: Represents a single run of the training of the particular player. This player is called a **trainee**. The run is accessed based on the access token obtained from the training instance instructor. The player enters the access token to the particular field and if the token is valid, the training run starts (behind the sciences, a sandbox is assigned to that training run from the pool that is associated with the particular training instance).

![kypo-basic-elements-training](img/KYPO-basic-elements-training.png)


### Overview 

The following picture displays all the core above-mentioned KYPO elements and the way they are interconnected.

![kypo-basic-elements-training](img/KYPO-basic-elements.png)
