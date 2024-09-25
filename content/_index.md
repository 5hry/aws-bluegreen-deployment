---
title : "Blue/Green Deployment"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Deploying an Amazon ECS service using a blue/green deployment

### Overall
In this section, we will implement this deployment strategy on AWS Cloud with the architecture shown below.

![Architecture](/images/main-arc.png)

A brief overview of the system: when users access the Internet, they pass through an Application Load Balancer that opens two ports, 80 and 81, pointing to two Target Groups registered with tasks in the ECS Service. Port 80 directs traffic to tasks running the production environment, while port 81 directs traffic to tasks running for testing. These tasks point to a database running on an EC2 instance.

As for Deployment, when code is pushed to Github, it triggers **CodeBuild** to rebuild a new image from the source code and then pushes the artifacts to S3 so that **CodeDeploy** can pull them and deploy them to the ECS Cluster. (Here, we are not using **CodeCommit** because it no longer supports new accounts, so we are using Github instead.)