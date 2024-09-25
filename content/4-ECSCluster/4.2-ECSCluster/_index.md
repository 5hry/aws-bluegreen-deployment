---
title : "Create ECS Service"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

Next, after creating the ECR to store the built images, we need to create an ECS Cluster to hold the service running the tasks for our application.

Now, I will create a cluster to hold the service running the tasks. Select Fargate mode.

![ECS 1](/images/4.ECS/01-ECS.png)

After creating the Cluster with basic configurations, create a service to deploy tasks with the launch type as Fargate in the newly created ECS Cluster.
![ECS 2](/images/4.ECS/02-ECS.png)

For Deployment configuration, select the service to launch a task group instead of a single task, which supports blue/green deployment. Here, we need to create a task definition that defines the virtual hardware and the container for the running task. You can create it in ECS or via JSON. It defines which image the container in the task will run, the container port, host port, etc.

![ECS 3](/images/4.ECS/03-ECS.png)

To interact with ECR, ECS, S3, ELB, etc., we need to create a role and assign it to CodeDeploy so it has the necessary permissions to pull images from ECR, deploy tasks in ECS, read the source from S3, and so on.

![ECS 4](/images/4.ECS/04-ECS.png)

In the networking section, select the security group as previously discussed. Since this Fargate needs to pull images from ECR, it requires public IP access to connect to the Internet, although this can be turned off if the route table and NAT gateway are reconfigured.

![ECS 5](/images/4.ECS/05-ECS.png)

Additionally, configure Load Balancing by selecting the Production listener added earlier as port 80 and the Test listener as port 81, forwarding traffic to the Blue and Green Target groups. 
We will select the ALB created in the previous section to forward traffic to the Blue and Green TGs.

![ECS 6](/images/4.ECS/06-ECS.png)
![ECS 7](/images/4.ECS/07-ECS.png)

After clicking **Create**, we now have a service with tasks in the pending state.
![ECS 8](/images/4.ECS/08-ECS.png)
