---
title : "Create Blue, Green Groups"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
Create two Target Groups, Blue and Green, to contain the tasks running the web application in the ECS Cluster. Here, select the target type as **IP Address** because the tasks will run in Fargate mode instead of EC2 instances.

![Target Groups 1](/images/3.ALB-TG/01-TG.png)

Open port 80 on both target groups.

![Target Groups 2](/images/3.ALB-TG/02-TG.png)

You can configure health checks to verify if the tasks registered in the TG are healthy. Health checks are available on the main page.

![Target Groups 3](/images/3.ALB-TG/03-TG.png)

Advanced settings for health checks.

![Target Groups 4](/images/3.ALB-TG/04-TG.png)

Now we have two target groups, Blue and Green. However, these two target groups are not yet associated with any Load Balancer. Therefore, we need to create an ALB to load traffic into these two TGs.

![Target Groups 5](/images/3.ALB-TG/05-TG.png)
