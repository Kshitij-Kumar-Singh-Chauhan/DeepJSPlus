<a name="readme-top"></a>
<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
  
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]


 <h1 align="center">DeepJS Plus</h1>
 
An upgraded **Deep** Learning-based **J**ob **S**cheduling implementation of DeepJS with several modifications to the original framework which include the use of a proximal policy gradients-based approach and a modified reward function to consider both average completion time and average slowdown as optimization goals.
<br>
<!-- TABLE OF CONTENTS -->
<details>
  <summary><b>Table of Contents</b></summary>
  <ol>
    <li><a href="#framework-overview">Framework Overview</a></li>
    <li><a href="#high-performance-simulation">High-Performance Simulation</a></li>
    <li><a href="#requirements">Requirements</a></li>
    <li><a href="#execution-and-setup">Execution and Setup</a></li>
    <li><a href="#results">Results</a></li>
  </ol>
</details>

## Framework Overview

The framework consists of two main packages: **core** and **playground**.

### a. Core Package

The **core** package abstracts and models entities involved in the data center job scheduling problem. It includes the following modules:

- **Config**: Provides configuration classes (TaskInstanceConfig, TaskConfig, JobConfig) for specifying resource requirements and durations of task instances, tasks, and jobs.
- **Job**: Models task instances, tasks, and jobs. The Job class maintains a collection of Task instances, and the Task class maintains a collection of TaskInstance instances. The state information of jobs and tasks is propagated through the entities.
- **Machine**: Models a machine in the data center.
- **Cluster**: Represents a computing cluster and maintains a list of machines.
- **Algorithm**: Defines the interface for scheduling algorithms. Users can implement custom scheduling algorithms by implementing this interface.
- **Scheduler**: Models the scheduler using the strategy pattern. Different instances of the Scheduler class can be used with different scheduling algorithms.
- **Broker**: Implements the class Broker, which replaces users in submitting jobs to the computing cluster.
- **Monitor**: Implements the class Monitor, used to monitor and record the simulation state.
- **Simulation**: Models a simulation. It requires constructing a Cluster instance, a series of JobConfig instances, and a Scheduler instance. Optionally, a Monitor instance can be used to monitor the simulation process.

### b. Playground Package

The **playground** package provides a convenient environment for conducting experiments within the framework. It contains two sub-packages: **DAG** and **Non-DAG**. These packages support simulation experiments considering dependencies between tasks and without considering dependencies between tasks, respectively.

Both sub-packages include pre-implemented heuristic job scheduling algorithms and job scheduling algorithms based on deep reinforcement learning. For example, the **Non-DAG/algorithm/DeepJS** directory contains the Data Center job scheduling algorithm based on deep reinforcement learning.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## High Performance Simulation

To achieve high-performance simulation, the framework utilizes several design choices:

- **TaskInstance as SimPy Process**: Conceptually, TaskInstance is designed as a SimPy Process, representing the actual resource consumer and executor of business logic in the data center. The Task and Job classes are designed as collections of TaskInstances. The framework utilizes Python's property feature to synthesize the states of tasks and jobs based on the forms of their respective TaskInstance instances. This design allows for efficient and accurate status retrieval, as the acquisition of task and job states is deferred until queried, minimizing active maintenance during simulation time steps.
- **SimPy Processes**: The Broker, Scheduler, and Monitor are also implemented as SimPy processes, enabling continuous submission of jobs, scheduling, and monitoring, respectively.
- **Strategy Pattern**: The strategy pattern is used to decouple the Scheduler implementation from the scheduling algorithm. The Scheduler class serves as the context, while the scheduling algorithms are implemented as separate strategy classes. This separation allows for easily adding or modifying scheduling algorithms without changing the original class or other strategies.
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Requirements

The framework has the following requirements:

- Python 3.6 or later
- SimPy 3.0.11
- TensorFlow 1.12.0
- NumPy 1.15.3
- Pandas 0.23.4

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Execution and Setup

To execute and set up the framework, follow these steps:
- Clone the codebase.
- Set the PYTHONPATH: Add the path to the project directory to the system environment variable PYTHONPATH. This step allows Python to locate the necessary modules and packages.
- Navigate to the codebase directory and execute the following command:
  
  ```sh
  cd DeepJSPlus/codebase
  python main_exec.py
  ```

You can adjust the script name or arguments according to your specific simulation requirements.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Results

The evaluation of the algorithm using simulation shows that it outperforms heuristic-based job scheduling algorithms and reduces the average completion time and slow down.
It also shows reduced makespan as compared to heuristic algorithms as shown in the table below.


| Algorithm | Average Makespan (s) |
|-----------|----------------------|
| Ours      | 626                  |
| First-Fit | 680                  |
| Tetris    | 689                  |


The following plot shows the improvement in completion time by using the proposed Proximal Policy Optimization in comparison to using Policy Gradient Method.

<p align="center">
<img src="https://github.com/Kshitij-Kumar-Singh-Chauhan/DeepJSPlus/blob/main/Images/Results/ComparisonPlot_CompletionTime.png" align="center" width="550">
</p>

It is expected that this algorithm can provide significant benefits in scenarios where job scheduling is critical to the overall performance of the system, such as in manufacturing, logistics, and data centers. The ability to optimize job scheduling policies in real time can potentially lead to significant improvements in efficiency and productivity, ultimately resulting in cost savings and improved energy efficiency.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

































<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/Kshitij-Kumar-Singh-Chauhan/DeepJSPlus/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/Kshitij-Kumar-Singh-Chauhan/DeepJSPlus/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/Kshitij-Kumar-Singh-Chauhan/DeepJSPlus/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/Kshitij-Kumar-Singh-Chauhan/DeepJSPlus/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/kshitijkumarsinghchauhan/

