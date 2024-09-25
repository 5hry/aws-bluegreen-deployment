---
title : "Preparation "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

{{% notice warning %}}
You need to have a web application ready; if you don't have one, you cannot proceed. You can refer to and use the web application [here](https://github.com/5hry/e-commerce-web-bluegreen-deploy)
{{% /notice %}}

This workshop requires the source code for a web application and a Dockerfile to build the application.
In this workshop, I will use a sales web application, specifically for electronic devices. It will connect to a database running on an EC2 Instance.

Since this workshop focuses on BlueGreenDeployment, I created an EC2 Instance to run the database to save resources.

I have prepared a Dockerfile to run the database from the source code above. You can download it to run or simply copy the DNS of the EC2 Instance I created here (**ec2-54-169-49-30.ap-southeast-1.compute.amazonaws.com**) into the `connectDB.php` file.
![Image](/images/2.prerequisite/001-connectDB.png)
The EC2 is running a database image for the application.
![Docker Database](/images/2.prerequisite/002-docker.png)

Now we can follow the steps in the workshop without worrying about missing anything.
