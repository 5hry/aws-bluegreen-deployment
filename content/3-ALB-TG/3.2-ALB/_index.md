---
title : "Create Application Load Balancer"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---
ALB is used to receive traffic directly from users, so we need to select the Internet Facing scheme, and for now, we only need IPv4.
![ALB 1](/images/3.ALB-TG/01-ALB.png)

Here, select all 3 zones in the Singapore region.

{{% notice tip %}}
Here, we need to select at least 2 zones, but the more, the better. For each zone we select, the ALB will place a ...(I forgot this part, I will research and update it) in the public subnet of that zone. Afterward, when traffic enters or exits the subnet of that zone, it will pass through that.
{{% /notice %}}
![ALB 2](/images/3.ALB-TG/02-ALB.png)

Create 2 listeners, where each listener will listen on a port on the ALB and then forward traffic to the corresponding TG. Here, port 80 will forward traffic to the Blue group, and port 81 will forward traffic to the Green group.

![ALB 3](/images/3.ALB-TG/03-ALB.png)

{{% notice warning %}}
In the Security group, you must open both port 80 for users and port 81 for those responsible for testing. If port 81 is not open, access to the testing environment will not be possible.
{{% /notice %}}

![ALB 4](/images/3.ALB-TG/04-ALB.png)

We can review an overview of the ALB we are about to create below. If there are any mistakes, they can be corrected before clicking **Create**.
![ALB 5](/images/3.ALB-TG/05-ALB.png)

After clicking **Create**, we will have the DNS name, and we can access it through this DNS name.

![ALB 6](/images/3.ALB-TG/06-ALB.png)
