### In this lab we create and edit a simple pipeline with parallel stages to build, test and deploy a simple-java-maven-app. 

### The lab demonstrates the concept of agents, nodes and executors

+ **The Jenkins controller** (formerly known as the Jenkins master) is the Jenkins service itself. It is a webserver that also acts as a brain for deciding how, when, and where to run tasks.

+ A **node** is a server where Jenkins runs tasks on executors. The Jenkins controller also runs on a node.

+ An **executor** is effectively a thread used to execute tasks

+ An *agent* is a tool that manages the executors on a remote node, on behalf of Jenkins.

## Objectives of the lab:
+ Defining global **agent none** meaning no default agent to use for all stages
+ Control the node on which a Pipeline or individual stages run
+ Build and run tests in parallel on two different agent environments: Running some stage builds on jdk7-node agent while other stage builds on jdk-8-node agent
+ setting stage-specific environment variables


Blue Ocean view               |    Stage view        | 
:-------------------------:|:-------------------------:|
![Pipleline Visualization](https://github.com/fred-juma/Certified-Jenkins-Administrator/blob/main/images/Lab02_stage_blue_ocean_view.JPG)|![Pipleline Visualization](https://github.com/fred-juma/Certified-Jenkins-Administrator/blob/main/images/Lab02_stage_build_stage_view.JPG)|


