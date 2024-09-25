+++
title = "Clean up resources"
date = 2022
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

As a result, we can access the website through the DNS name of the ALB.
![Result](/images/6.clean/result.png)

Above are the detailed steps to deploy an ECS service using the Blue/Green Deployment strategy. You can access it via [ALB DNS](http://ws1-bluegreen-alb-1574488828.ap-southeast-1.elb.amazonaws.com/). Next, I will enhance and develop it further by using Route53 to optimize traffic routing.

In the resource cleanup section, we can leave a few services like CodeBuild, CodeDeploy, and CodePipeline, as these services are pay-per-use, so they can be retained for future purposes. For ECS, we can set the desired task count to 0, which incurs almost no cost. This is an efficient way to pause the workshop temporarily and resume it later. 
Additionally, we can delete resources like ALB, TG, etc.
Select the ALB and confirm deletion.
![ALB 1](/images/6.clean/01-ALB.png)
![ALB 2](/images/6.clean/02-alb.png)
![ALB 3](/images/6.clean/03-alb.png)

If you created an EC2 instance for running the database, delete the EC2 instance. Select EC2 and choose **Stop** if you need it for later use, otherwise, **Terminate** it.
![EC2 1](/images/6.clean/01-ec2.png)

Finally, if you have created too many images in ECR, consider deleting them, leaving only the latest image for future use.
![ECR 1](/images/6.clean/01-ECR.png)

Delete old Task Definitions if not needed, and deregister the old Tasks.
![Task def 1](/images/6.clean/01-task.png)

So, I have completed the resource cleanup. Thank you for reading. If you have any feedback, feel free to contact me via [this Facebook link](https://www.facebook.com/stn.akai).
