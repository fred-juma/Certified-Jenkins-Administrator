#### In this lab we create and edit a simple pipeline with parallel stages to build, test and deploy a simple-java-maven-app. 

#### The lab demonstrates the concept of interractive input, stash and unstash

+ **stash** step is used to save a set of files for use later in the same build, but in another stage that executes on a different node/workspace

+ **unstash** step is used to restore the stashed files into the current workspace of the other stage.

#### Stashed files are archived in a compressed tar file, which works well for small (<5 Mb) files. 

#### Stashing large files consumes significant resources (especially CPU) on both the master and agent nodes.

#### For large files, consider using one of the following options:

+ The *External Workspace manager* plugin
+ An external repository manager such as *Nexus* or *Artifactory*
+ The *Artifact Manager on S3* plugin

#### Wait for interactive input: A common practice is to run a wait-for-input stage after all tests have run successfully, to have someone confirm that the software should be deployed

#### Lab Objectives

+ use stash and unstash to ensure that the JDK 7 build is used by the JDK 7 test stage and the JDK 8 build is used by the JDK 8 test stage
+ use *Wait for interactive input* step to  pause the Pipeline to wait for input from a human

Wait for interactive input               |    Stage view        | 
:-------------------------:|:-------------------------:|
![Pipleline Visualization](https://github.com/fred-juma/Certified-Jenkins-Administrator/blob/main/images/Lab03-interractive-input.JPG)|![Pipleline Visualization](https://github.com/fred-juma/Certified-Jenkins-Administrator/blob/main/images/Lab03_stash_unstash_stage_view.JPG)|


