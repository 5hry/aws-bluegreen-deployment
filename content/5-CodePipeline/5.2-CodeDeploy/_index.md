---
title : "Create CodeDeploy"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

After creating the Build Project, we will create CodeDeploy to take the image built from the Build Project and deploy it to run tasks in the two targets **Blue** and **Green**.

In CodeDeploy, create an application with the platform **Amazon ECS**.
![CodeDeploy 1](/images/5.Codepipeline/01-CD.png)

From the newly created application, create a deployment group to hold the deployments.
![CodeDeploy 2](/images/5.Codepipeline/02-CD.png)

The role assigned here needs permissions to read from ECR, deploy ECS tasks, read S3, and manage ALB traffic.
![CodeDeploy role](/images/5.Codepipeline/role-CD.png)

Next, configure the information for the cluster, service, ALB, etc. Select the Cluster and Service created in the previous section, along with the ALB and Target Groups created in section 2.
![CodeDeploy 3](/images/5.Codepipeline/03-CD.png)

Here, you can configure the deployment in multiple ways, such as rerouting traffic immediately after the new tasks are created or configuring the time to reroute traffic, rerouting strategies, and terminating tasks running the old version.
![CodeDeploy 4](/images/5.Codepipeline/05-CD.png)

Select **Create Deployment Group** to complete the creation.

When deploying, CloudFormation will be initiated to create resources on ECS.

