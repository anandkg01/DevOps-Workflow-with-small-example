# DevOps-Workflow-with-small-example

Below diagram depicts complete DevOps workflow:

![alt text](https://github.com/anandkg01/DevOps-Workflow-with-small-example/blob/main/IMG_20220207_170405_194.jpg?raw=true)

Following tools are used for this Workflow:

    Jenkins to create build pipeline (pipeline as code)
    Git for source control
    Maven to build the source
    Selenium for automated testing
    Docker for containerization of the tool and pushing the docker image to dockerhub
    Puppet for distributing tool across agents
    Nagios for monitoring the tool

In my example I have considered a web application, which would be built, tested, deployed and monitored using above mentioned DevOps tools and technologies. I have used Ubuntu OS for the complete workflow.


 I have created a Jenkins pipeline with following stages:

    Checkout source from Git
    Compile the code using Maven
    Do automated tests
    Generate Cobertura report
    Package the archieve in war and deploy to Puppet master machine
    Build the docker image of war on top of Tomcat as base image
    Deploy the docker image to DockerHub

[Here is the Jenkins pipeline script for same](https://github.com/anandkg01/DevOps-Workflow-with-small-example/blob/main/Jenkinsfile)

[Here is the Dockerfile of the image](https://github.com/anandkg01/DevOps-Workflow-with-small-example/blob/main/Dockerfile)

We can also distribute the war file to other machines using Puppet Configuration management tool. Follow the below steps:

    Install Puppet Master in Master machine and Puppet Agent in Agent machine.
    Modify Puppet Manifest file to install Tomcat package and copy the generated war file from the build
    Apply the manifest in Puppet Agent machine to spin up the web application

[Here is the Puppet config file for the same:](https://github.com/anandkg01/DevOps-Workflow-with-small-example/blob/main/site.pp)

Now we can use Nagios monitoring tool to monitor our application

    Install Nagios in Master machine and NRPE plugin in Agent machine
    Create a host.cfg file in Master machine to to monitor the Agent machine
    Configure host.cfg to monitor PING and SSH services of Agent machine

[Here is the Nagios config file](https://github.com/anandkg01/DevOps-Workflow-with-small-example/blob/main/host.cfg)

With this we have completed the DevOps tool chain with small example.


For configuration management there are other tools also available for e.g. Ansible, Salt etc. Depending on our need whether we need push or pull architecture we can choose these tools.

We have Kubernetes, the container orchestration tool which is a platform designed to completely manage the life cycle of containerized applications and services using methods that provide predictability, scalability, and high availability. With Kubernetes we can build self healing infrastructure, where in if one node (machine) dies another automatically builds up. 

The DevOps Ecosystem is very vast and growing rapidly with new tools and technologies. Based on our needs, we can choose the right tools and automate our deliveries!

